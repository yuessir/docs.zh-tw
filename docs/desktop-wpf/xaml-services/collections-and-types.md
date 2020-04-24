---
title: XAML 的集合和集合類型
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 2ec58026c605df31489c8aab4c4cc714dab11474
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "82071294"
---
# <a name="collections-and-collection-types-for-xaml"></a><span data-ttu-id="b3ffe-102">XAML 的收集類型</span><span class="sxs-lookup"><span data-stu-id="b3ffe-102">Collections and collection types for XAML</span></span>

<span data-ttu-id="b3ffe-103">本文介紹如何定義旨在支援集合的類型的屬性,並支援 XAML 語法,以便將集合項實例化為父物件元素或屬性元素的元素子級。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-103">This article describes how to define properties of types that are intended to support a collection, and to support the XAML syntax for instantiating collection items as element children of a parent object element or property element.</span></span>

## <a name="xaml-collection-concepts"></a><span data-ttu-id="b3ffe-104">XAML 收集概念</span><span class="sxs-lookup"><span data-stu-id="b3ffe-104">XAML Collection Concepts</span></span>

<span data-ttu-id="b3ffe-105">從概念上講,XAML 中任何在 XAML 物件元素或 XAML 屬性元素範圍內有多個子項的關係都必須作為集合實現。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-105">Conceptually, any relationship in XAML where there are multiple child items within the scope of a XAML object element or XAML property element must be implemented as a collection.</span></span> <span data-ttu-id="b3ffe-106">該集合必須與 XAML 類型的特定 XAML 屬性相關聯,該屬性是該關係中的父級。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-106">That collection must be associated with a particular XAML property of the XAML type that is the parent in that relationship.</span></span> <span data-ttu-id="b3ffe-107">屬性必須是集合,因為 XAML 處理器希望將標記中的每個項分配為備份集合屬性的新添加項。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-107">The property must be a collection because a XAML processor expects to assign each item in markup to be a newly added item of the backing collection property.</span></span>

<span data-ttu-id="b3ffe-108">在 XAML 語言級別,收集支持的確切要求尚未完全定義。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-108">At the XAML language level, the exact requirements of collection support are not fully defined.</span></span> <span data-ttu-id="b3ffe-109">集合可以是清單或字典(但不能同時兩者)的概念在 XAML 語言級別定義,但哪些支援類型表示列表或字典不是由 XAML 語言定義的。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-109">The concept that a collection can be either a list or a dictionary(but not both) is defined at the XAML language level, but which backing types represent either lists or dictionaries is not defined by the XAML language.</span></span>

<span data-ttu-id="b3ffe-110">在 .NET XAML 服務中,XAML 集合支援的概念在 .NET 支援類型方面定義得更清晰。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-110">In .NET XAML Services, the concept of XAML collection support is more clearly defined in terms of .NET backing types.</span></span> <span data-ttu-id="b3ffe-111">具體來說,XAML 對集合的支援基於幾個 .NET 概念和 API,這些概念和 API 用於一般清單和字典 .NET 程式設計。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-111">Specifically, the XAML support for collections is based on several .NET concepts and APIs that are used for lists and dictionaries in general .NET programming.</span></span>

1. <span data-ttu-id="b3ffe-112">介面<xref:System.Collections.IList>指示清單集合。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-112">The <xref:System.Collections.IList> interface indicates a list collection.</span></span>

2. <span data-ttu-id="b3ffe-113">介面<xref:System.Collections.IDictionary>指示字典集合。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-113">The <xref:System.Collections.IDictionary> interface indicates a dictionary collection.</span></span>

3. <span data-ttu-id="b3ffe-114"><xref:System.Array>表示陣列,陣組支援<xref:System.Collections.IList>方法。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-114"><xref:System.Array> represents an array, and an array supports <xref:System.Collections.IList> methods.</span></span>

<span data-ttu-id="b3ffe-115">在這些集合概念中,.NET XAML 服務 XAML`Add`處理器期望在集合屬性類型的特定實例上調用 該方法。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-115">In each of these collection concepts, a .NET XAML Services XAML processor expects to call the `Add` method on a specific instance of the collection property's type.</span></span> <span data-ttu-id="b3ffe-116">或者,在序列化方案中,XAML 處理器根據每個集合的特定概念"Item"為每個在清單、字典或陣列中找到的每個項生成離散的 XAML 類型實例。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-116">Or, in a serialization scenario, a XAML processor produces discrete XAML-type instances for each item found in the list, dictionary, or array based on each collection's specific concept of "Items".</span></span> <span data-ttu-id="b3ffe-117">這些項目是: <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType><xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>;的顯式<xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> <xref:System.Array> 。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-117">These items are: <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType>; <xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>; the explicit <xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> for <xref:System.Array>.</span></span>

## <a name="generic-collections"></a><span data-ttu-id="b3ffe-118">通用集合</span><span class="sxs-lookup"><span data-stu-id="b3ffe-118">Generic Collections</span></span>

<span data-ttu-id="b3ffe-119">泛型集合可用於常規 .NET 程式設計,也可用於 XAML 集合屬性。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-119">Generic collections can be useful for general .NET programming, and can also be used for XAML collection properties.</span></span> <span data-ttu-id="b3ffe-120">但是,泛型介面<xref:System.Collections.Generic.IList%601>和<xref:System.Collections.Generic.IDictionary%602>.NET XAML 服務 XAML 處理器未識別為<xref:System.Collections.IList>等<xref:System.Collections.IDictionary>效於非泛型或 。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-120">However, the generic interfaces <xref:System.Collections.Generic.IList%601> and <xref:System.Collections.Generic.IDictionary%602> are not identified by .NET XAML Services XAML processors as being equivalent to the non-generic <xref:System.Collections.IList> or <xref:System.Collections.IDictionary>.</span></span> <span data-ttu-id="b3ffe-121">泛型集合屬性類型的推薦方法是從類<xref:System.Collections.Generic.List%601><xref:System.Collections.Generic.Dictionary%602>或 派生,而不是實現介面。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-121">Rather than implementing the interfaces, a recommended approach for generic collection property types is to derive from the classes <xref:System.Collections.Generic.List%601> or <xref:System.Collections.Generic.Dictionary%602>.</span></span> <span data-ttu-id="b3ffe-122">這些類實現非泛型介面,從而在基本實現中包括對 XAML 集合的預期支援。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-122">These classes implement the non-generic interfaces and thus include the expected support for XAML collections in the base implementation.</span></span>

## <a name="read-only-collections-and-initialization-logic"></a><span data-ttu-id="b3ffe-123">唯讀取與初始化邏輯</span><span class="sxs-lookup"><span data-stu-id="b3ffe-123">Read-Only Collections and Initialization Logic</span></span>

<span data-ttu-id="b3ffe-124">在 .NET 程式設計中,將保存集合值的任何屬性作為唯讀集合,是一種常見的設計模式。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-124">In .NET programming, it is a common design pattern to make any property that holds a value of a collection as a read-only collection.</span></span> <span data-ttu-id="b3ffe-125">此模式允許擁有集合屬性的實例更好地控制集合發生的情況。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-125">This pattern permits the instance that owns the collection property to better control what happens to the collection..</span></span> <span data-ttu-id="b3ffe-126">具體而言,該模式通過設置屬性防止意外替換整個預先存在的集合。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-126">Specifically, the pattern prevents accidental replacement of the entire pre-existing collection by setting the property.</span></span> <span data-ttu-id="b3ffe-127">在此模式中,調用方對集合的任何訪問都應該通過調用集合類型和/或相關集合介面(如<xref:System.Collections.IList>) 支援的方法或屬性進行。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-127">In this pattern, any access to the collection by callers should instead be made by calling methods or properties as supported by the collection type and/or the relevant collection interfaces such as <xref:System.Collections.IList>.</span></span>

<span data-ttu-id="b3ffe-128">使用此模式意味著公開唯讀集合屬性的任何類必須首先初始化該屬性以容納空集合。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-128">Using this pattern implies that any class that exposes a read-only collection property must first initialize that property to hold an empty collection.</span></span> <span data-ttu-id="b3ffe-129">通常,初始化是作為類構造行為的一部分執行的。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-129">Typically the initialization is performed as part of the construction behavior for the class.</span></span> <span data-ttu-id="b3ffe-130">為了對 XAML 有用,無參數構造函數始終引用此類邏輯非常重要,因為 XAML 在處理屬性(集合屬性或其他)之前通常調用無參數構造函數。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-130">To be useful for XAML, it is important that such logic is always referenced by the parameterless constructor, because XAML generally calls the parameterless constructor prior to processing the properties (collection properties or otherwise).</span></span>

## <a name="xaml-type-system-support-and-collections"></a><span data-ttu-id="b3ffe-131">XAML 類型系統支援和集合</span><span class="sxs-lookup"><span data-stu-id="b3ffe-131">XAML Type System Support and Collections</span></span>

<span data-ttu-id="b3ffe-132">除了解析 XAML 和填充或序列化集合屬性的基本機制外,.NET XAML 服務中實現的 XAML 類型系統還包括與 XAML 中的集合相關的多個設計功能。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-132">Beyond the basic mechanics of parsing XAML and populating or serializing collection properties, the XAML type system as implemented in .NET XAML Services includes several design features that pertain to collections in XAML.</span></span>

1. <span data-ttu-id="b3ffe-133"><xref:System.Xaml.XamlType.IsCollection%2A>如果 XAML 類型由提供 XAML 集合支援的類型支援,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-133"><xref:System.Xaml.XamlType.IsCollection%2A> returns true if the XAML type is backed by a type that provides XAML collection support.</span></span>

2. <span data-ttu-id="b3ffe-134"><xref:System.Xaml.XamlType.IsDictionary%2A>並<xref:System.Xaml.XamlType.IsArray%2A>可以進一步識別 XAML 類型支援的集合模式。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-134"><xref:System.Xaml.XamlType.IsDictionary%2A> and <xref:System.Xaml.XamlType.IsArray%2A> can further identify which collection mode the XAML type supports.</span></span> <span data-ttu-id="b3ffe-135">對於基於 .NET XAML 服務和 XAML 類型<xref:System.Xaml.XamlWriter>系統但不基於現有 實現的自定義 XAML 處理器,可能需要瞭解使用哪種收集模式,以便知道要調用哪種方法來進行收集處理。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-135">For custom XAML processors that are based on .NET XAML Services and the XAML type system but not based on existing <xref:System.Xaml.XamlWriter> implementations, knowing which collection mode is used might be necessary in order to know which method to invoke for collection processing.</span></span>

3. <span data-ttu-id="b3ffe-136">以前的每個屬性值都可能受 XAML<xref:System.Xaml.XamlType.LookupCollectionKind%2A>類型的 重寫的影響。</span><span class="sxs-lookup"><span data-stu-id="b3ffe-136">Each of the previous property values is potentially influenced by overrides of <xref:System.Xaml.XamlType.LookupCollectionKind%2A> on a XAML type.</span></span>