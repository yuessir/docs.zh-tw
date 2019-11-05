---
title: 教學課程：預測自行車出租需求-時間序列
description: 本教學課程說明如何使用單一變數時間序列分析和 ML.NET，預測自行車出租服務的需求。
ms.date: 10/31/2019
ms.topic: tutorial
ms.custom: mvc
ms.author: luquinta
author: luisquintanilla
ms.openlocfilehash: f30aac5f8467c2410e9008bafea3cf35af3f4e2a
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/01/2019
ms.locfileid: "73425636"
---
# <a name="tutorial-forecast-bike-rental-service-demand-with-time-series-analysis-and-mlnet"></a><span data-ttu-id="d5ee8-103">教學課程：使用時間序列分析和 ML.NET 預測自行車出租服務需求</span><span class="sxs-lookup"><span data-stu-id="d5ee8-103">Tutorial: Forecast bike rental service demand with time series analysis and ML.NET</span></span>

<span data-ttu-id="d5ee8-104">瞭解如何使用單一變數時間序列分析，針對儲存在含有 ML.NET 之 SQL Server 資料庫中的資料，預測自行車出租服務的需求。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-104">Learn how to forecast demand for a bike rental service using univariate time series analysis on data stored in a SQL Server database with ML.NET.</span></span>

<span data-ttu-id="d5ee8-105">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> * <span data-ttu-id="d5ee8-106">了解問題</span><span class="sxs-lookup"><span data-stu-id="d5ee8-106">Understand the problem</span></span>
> * <span data-ttu-id="d5ee8-107">從資料庫載入資料</span><span class="sxs-lookup"><span data-stu-id="d5ee8-107">Load data from a database</span></span>
> * <span data-ttu-id="d5ee8-108">建立預測模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-108">Create a forecasting model</span></span>
> * <span data-ttu-id="d5ee8-109">評估預測模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-109">Evaluate forecasting model</span></span>
> * <span data-ttu-id="d5ee8-110">儲存預測模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-110">Save a forecasting model</span></span>
> * <span data-ttu-id="d5ee8-111">使用預測模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-111">Use a forecasting model</span></span>

> [!NOTE]
> <span data-ttu-id="d5ee8-112">本教學課程使用 DatabaseLoader 的預覽版本。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-112">This tutorial uses a preview version of DatabaseLoader.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5ee8-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d5ee8-113">Prerequisites</span></span>

- <span data-ttu-id="d5ee8-114">已安裝「.NET Core 跨平台開發」工作負載的 [Visual Studio 2017 15.6 或更新版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-114">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.</span></span>

## <a name="time-series-forecasting-sample-overview"></a><span data-ttu-id="d5ee8-115">時間序列預測範例總覽</span><span class="sxs-lookup"><span data-stu-id="d5ee8-115">Time series forecasting sample overview</span></span>

<span data-ttu-id="d5ee8-116">這個範例是一個 **C# .net Core 主控台應用程式**，使用單一變數時間序列分析演算法（稱為單一頻譜分析）來預測自行車出租的需求。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-116">This sample is a **C# .NET Core console application** that forecasts demand for bike rentals using a univariate time series analysis algorithm known as Single Spectrum Analysis.</span></span> <span data-ttu-id="d5ee8-117">此範例的程式碼可在 GitHub 上的[dotnet/machinelearning 範例](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand)存放庫中找到。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-117">The code for this sample can be found on the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand) repository on GitHub.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="d5ee8-118">了解問題</span><span class="sxs-lookup"><span data-stu-id="d5ee8-118">Understand the problem</span></span>

<span data-ttu-id="d5ee8-119">為了執行有效率的作業，清查管理扮演重要的角色。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-119">In order to run an efficient operation, inventory management plays a key role.</span></span> <span data-ttu-id="d5ee8-120">存貨中有太多產品，表示坐在貨架上的 unsold 產品不會產生任何收益。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-120">Having too much of a product in stock means unsold products sitting on the shelves not generating any revenue.</span></span> <span data-ttu-id="d5ee8-121">產品過少會導致銷售和客戶從競爭者購買。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-121">Having too little product leads to lost sales and customers purchasing from competitors.</span></span> <span data-ttu-id="d5ee8-122">因此，常數的問題是，最適合的清查數量為何？</span><span class="sxs-lookup"><span data-stu-id="d5ee8-122">Therefore, the constant question is, what is the optimal amount of inventory to keep on hand?</span></span> <span data-ttu-id="d5ee8-123">時間序列分析會查看歷程記錄資料、識別模式，並使用此資訊來預測未來一些時間的值，以協助提供這些問題的答案。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-123">Time-series analysis helps provide an answer to these questions by looking at historical data, identifying patterns, and using this information to forecast values some time in the future.</span></span> 

<span data-ttu-id="d5ee8-124">分析本教學課程中使用的資料的技術是單一變數時間序列分析。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-124">The technique for analyzing data used in this tutorial is univariate time-series analysis.</span></span> <span data-ttu-id="d5ee8-125">單一變數時間序列分析會以特定間隔（例如每月銷售），查看一段時間內的單一數值觀察。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-125">Univariate time-series analysis takes a look at a single numerical observation over a period of time at specific intervals such as monthly sales.</span></span> 

<span data-ttu-id="d5ee8-126">本教學課程中使用的演算法是[單一頻譜分析（SSA）](http://ssa.cf.ac.uk/zhigljavsky/pdfs/SSA/SSA_encyclopedia.pdf)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-126">The algorithm used in this tutorial is [Single Spectrum Analysis(SSA)](http://ssa.cf.ac.uk/zhigljavsky/pdfs/SSA/SSA_encyclopedia.pdf).</span></span> <span data-ttu-id="d5ee8-127">SSA 的運作方式是將時間序列分解成一組主要元件。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-127">SSA works by decomposing a time-series into a set of principal components.</span></span> <span data-ttu-id="d5ee8-128">這些元件可以解讀為與趨勢、雜訊、季節性和許多其他因素相對應的信號部分。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-128">These components can be interpreted as the parts of a signal that correspond to trends, noise, seasonality, and many other factors.</span></span> <span data-ttu-id="d5ee8-129">然後，系統會重建這些元件，並用來預測未來一些時間的值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-129">Then, these components are reconstructed and used to forecast values some time in the future.</span></span>

## <a name="create-console-application"></a><span data-ttu-id="d5ee8-130">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="d5ee8-130">Create console application</span></span>

1. <span data-ttu-id="d5ee8-131">建立名為 "BikeDemandForecasting" 的新 **C# .net Core 主控台應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-131">Create a new **C# .NET Core console application** called "BikeDemandForecasting".</span></span>
1. <span data-ttu-id="d5ee8-132">安裝**Microsoft.ML**版本**1.4.0-preview2** NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="d5ee8-132">Install **Microsoft.ML** version **1.4.0-preview2** NuGet package</span></span>
    1. <span data-ttu-id="d5ee8-133">在 [方案總管] 中，於您的專案上按一下滑鼠右鍵，然後選取 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-133">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span>
    1. <span data-ttu-id="d5ee8-134">選擇 [nuget.org] 作為 [套件來源]，選取 [**流覽**] 索引標籤，搜尋**Microsoft.ML**。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-134">Choose "nuget.org" as the Package source, select the **Browse** tab, search for **Microsoft.ML**.</span></span>
    1. <span data-ttu-id="d5ee8-135">勾選 [**包含發行**前版本] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-135">Check the **Include prerelease** checkbox.</span></span>
    1. <span data-ttu-id="d5ee8-136">選取 [安裝] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-136">Select the **Install** button.</span></span>
    1. <span data-ttu-id="d5ee8-137">在 [預覽變更] 對話方塊上，選取 [確定] 按鈕，然後在 [授權接受] 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-137">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the License Acceptance dialog if you agree with the license terms for the packages listed.</span></span>
    1. <span data-ttu-id="d5ee8-138">針對**SqlClient**版本**4.7.0**、 **0.16.0 版本-preview2**和版本**時間序列-1.4.0** **，重複**這些步驟 **：。**</span><span class="sxs-lookup"><span data-stu-id="d5ee8-138">Repeat these steps for **System.Data.SqlClient** version **4.7.0**, **Microsoft.ML.Experimental** version **0.16.0-preview2**, and **Microsoft.ML.TimeSeries** version **1.4.0-preview2**.</span></span>

### <a name="prepare-and-understand-the-data"></a><span data-ttu-id="d5ee8-139">準備並了解資料</span><span class="sxs-lookup"><span data-stu-id="d5ee8-139">Prepare and understand the data</span></span>

1. <span data-ttu-id="d5ee8-140">建立名為*Data*的目錄。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-140">Create a directory called *Data*.</span></span>
1. <span data-ttu-id="d5ee8-141">下載[ *DailyDemand .mdf*資料庫](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Data/DailyDemand.mdf)檔案，並將它儲存至*資料*目錄。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-141">Download the [*DailyDemand.mdf* database file](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Data/DailyDemand.mdf) and save it to the *Data* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="d5ee8-142">本教學課程中使用的資料來自[UCI 自行車共用資料集](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-142">The data used in this tutorial comes from the [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset).</span></span> <span data-ttu-id="d5ee8-143">Fanaee-T、Hadi 和 Gama、Joao、「結合集團偵測器和背景知識的事件標記」、人工智慧中的進度（2013）： pp 1-15、Springer link 柏林 Heidelberg、 [Web 連結](https://link.springer.com/article/10.1007%2Fs13748-013-0040-3)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-143">Fanaee-T, Hadi, and Gama, Joao, 'Event labeling combining ensemble detectors and background knowledge', Progress in Artificial Intelligence (2013): pp. 1-15, Springer Berlin Heidelberg, [Web Link](https://link.springer.com/article/10.1007%2Fs13748-013-0040-3).</span></span>

<span data-ttu-id="d5ee8-144">原始資料集包含數個對應至季節性和氣象的資料行。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-144">The original dataset contains several columns corresponding to seasonality and weather.</span></span> <span data-ttu-id="d5ee8-145">為了簡潔起見，因為本教學課程中使用的演算法只需要單一數值資料行中的值，所以原始資料集已壓縮成隻包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-145">For brevity and because the algorithm used in this tutorial only requires the values from a single numerical column, the original dataset has been condensed to include only the following columns:</span></span>  

- <span data-ttu-id="d5ee8-146">**dteday**：觀察的日期。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-146">**dteday**: The date of the observation.</span></span>
- <span data-ttu-id="d5ee8-147">**year**：觀察的編碼年份（0 = 2011，1 = 2012）。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-147">**year**: The encoded year of the observation (0=2011, 1=2012).</span></span>
- <span data-ttu-id="d5ee8-148">**cnt**：當天的自行車租用總數。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-148">**cnt**: The total number of bike rentals for that day.</span></span>

<span data-ttu-id="d5ee8-149">原始資料集會對應到在 SQL Server 資料庫中具有下列架構的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-149">The original dataset is mapped to a database table with the following schema in a SQL Server database.</span></span>

```SQL
CREATE TABLE [Rentals] (
    [RentalDate] DATE NOT NULL,
    [Year] INT NOT NULL,
    [TotalRentals] INT NOT NULL
);
```

<span data-ttu-id="d5ee8-150">以下是資料的範例：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-150">The following is a sample of the data:</span></span>

| <span data-ttu-id="d5ee8-151">RentalDate</span><span class="sxs-lookup"><span data-stu-id="d5ee8-151">RentalDate</span></span> | <span data-ttu-id="d5ee8-152">Year</span><span class="sxs-lookup"><span data-stu-id="d5ee8-152">Year</span></span> | <span data-ttu-id="d5ee8-153">TotalRentals</span><span class="sxs-lookup"><span data-stu-id="d5ee8-153">TotalRentals</span></span> |
| --- | --- | --- |
|<span data-ttu-id="d5ee8-154">1/1/2011</span><span class="sxs-lookup"><span data-stu-id="d5ee8-154">1/1/2011</span></span>|<span data-ttu-id="d5ee8-155">0</span><span class="sxs-lookup"><span data-stu-id="d5ee8-155">0</span></span>|<span data-ttu-id="d5ee8-156">985</span><span class="sxs-lookup"><span data-stu-id="d5ee8-156">985</span></span>|
|<span data-ttu-id="d5ee8-157">1/2/2011</span><span class="sxs-lookup"><span data-stu-id="d5ee8-157">1/2/2011</span></span>|<span data-ttu-id="d5ee8-158">0</span><span class="sxs-lookup"><span data-stu-id="d5ee8-158">0</span></span>|<span data-ttu-id="d5ee8-159">801</span><span class="sxs-lookup"><span data-stu-id="d5ee8-159">801</span></span>|
|<span data-ttu-id="d5ee8-160">1/3/2011</span><span class="sxs-lookup"><span data-stu-id="d5ee8-160">1/3/2011</span></span>|<span data-ttu-id="d5ee8-161">0</span><span class="sxs-lookup"><span data-stu-id="d5ee8-161">0</span></span>|<span data-ttu-id="d5ee8-162">1349</span><span class="sxs-lookup"><span data-stu-id="d5ee8-162">1349</span></span>|

### <a name="create-input-and-output-classes"></a><span data-ttu-id="d5ee8-163">建立輸入和輸出類別</span><span class="sxs-lookup"><span data-stu-id="d5ee8-163">Create input and output classes</span></span>

1. <span data-ttu-id="d5ee8-164">開啟*Program.cs*檔案，並以下列內容取代現有的 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-164">Open *Program.cs* file and replace the existing `using` statements with the following:</span></span>

    [!code-csharp [ProgramUsings](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L1-L8)]

1. <span data-ttu-id="d5ee8-165">建立 `ModelInput` 類別。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-165">Create `ModelInput` class.</span></span> <span data-ttu-id="d5ee8-166">在 `Program` 類別底下，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-166">Below the `Program` class, add the following code.</span></span>

    [!code-csharp [ModelInputClass](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L120-L127)]    

    <span data-ttu-id="d5ee8-167">`ModelInput` 類別包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-167">The `ModelInput` class contains the following columns:</span></span>

    - <span data-ttu-id="d5ee8-168">**RentalDate**：觀察的日期。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-168">**RentalDate**: The date of the observation.</span></span>
    - <span data-ttu-id="d5ee8-169">**Year**：觀察的編碼年份（0 = 2011，1 = 2012）。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-169">**Year**: The encoded year of the observation (0=2011, 1=2012).</span></span>
    - <span data-ttu-id="d5ee8-170">**TotalRentals**：當天的自行車租金總數。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-170">**TotalRentals**: The total number of bike rentals for that day.</span></span>

1. <span data-ttu-id="d5ee8-171">在新建立的 `ModelInput` 類別底下建立 `ModelOutput` 類別。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-171">Create `ModelOutput` class below the newly created `ModelInput` class.</span></span>

    [!code-csharp [ModelOutputClass](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L129-L136)]

    <span data-ttu-id="d5ee8-172">`ModelOutput` 類別包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-172">The `ModelOutput` class contains the following columns:</span></span>

    - <span data-ttu-id="d5ee8-173">**ForecastedRentals**：預測週期的預測值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-173">**ForecastedRentals**: The predicted values for the forecasted period.</span></span>
    - <span data-ttu-id="d5ee8-174">**LowerBoundRentals**：預測週期的預測最小值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-174">**LowerBoundRentals**: The predicted minimum values for the forecasted period.</span></span>
    - <span data-ttu-id="d5ee8-175">**UpperBoundRentals**：預測週期的預測最大值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-175">**UpperBoundRentals**: The predicted maximum values for the forecasted period.</span></span>

### <a name="define-paths-and-initialize-variables"></a><span data-ttu-id="d5ee8-176">定義路徑和初始化變數</span><span class="sxs-lookup"><span data-stu-id="d5ee8-176">Define paths and initialize variables</span></span>

1. <span data-ttu-id="d5ee8-177">在 `Main` 方法中，定義變數以儲存資料的位置、連接字串，以及要在何處儲存定型的模型。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-177">Inside the `Main` method, define variables to store the location of your data, connection string, and where to save the trained model.</span></span>

    [!code-csharp [DefinePaths](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L16-L19)]

1. <span data-ttu-id="d5ee8-178">藉由將下列這一行新增至 `Main` 方法，以[`MLContext`](xref:Microsoft.ML.MLContext)的新實例初始化 `mlContext` 變數。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-178">Initialize the `mlContext` variable with a new instance of [`MLContext`](xref:Microsoft.ML.MLContext) by adding the following line to the `Main` method.</span></span>

    [!code-csharp [MLContext](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L21)]

    <span data-ttu-id="d5ee8-179">[`MLContext`](xref:Microsoft.ML.MLContext)類別是所有 ML.NET 作業的起點，而初始化 mlCoNtext 會建立可在模型建立工作流程物件之間共用的新 ML.NET 環境。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-179">The [`MLContext`](xref:Microsoft.ML.MLContext) class is a starting point for all ML.NET operations, and initializing mlContext creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="d5ee8-180">就概念而言，類似於 Entity Framework 中的 `DBContext`。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-180">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="d5ee8-181">載入資料</span><span class="sxs-lookup"><span data-stu-id="d5ee8-181">Load the data</span></span>

1. <span data-ttu-id="d5ee8-182">建立 `DatabaseLoader`，以載入 `ModelInput`類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-182">Create `DatabaseLoader` that loads records of type `ModelInput`.</span></span>

    [!code-csharp [CreateDBLoader](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L23)]

1. <span data-ttu-id="d5ee8-183">定義要從資料庫載入資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-183">Define the query to load the data from the database.</span></span>

    [!code-csharp [DefineSQLQuery](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L25)]

    <span data-ttu-id="d5ee8-184">ML.NET 演算法預期資料的類型[`Single`](xref:System.Single)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-184">ML.NET algorithms expect data to be of type [`Single`](xref:System.Single).</span></span> <span data-ttu-id="d5ee8-185">因此，來自資料庫的數值若不是[`Real`](xref:System.Data.SqlDbType)的類型，則必須將單精確度浮點數轉換成[`Real`](xref:System.Data.SqlDbType)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-185">Therefore, numerical values coming from the database that are not of type [`Real`](xref:System.Data.SqlDbType), a single-precision floating-point value, have to be converted to [`Real`](xref:System.Data.SqlDbType).</span></span> 

    <span data-ttu-id="d5ee8-186">[`Year`] 和 [`TotalRental`] 資料行都是資料庫中的兩個整數類型。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-186">The `Year` and `TotalRental` columns are both integer types in the database.</span></span> <span data-ttu-id="d5ee8-187">使用 `CAST` 內建函數時，它們都會轉換成 `Real`。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-187">Using the `CAST` built-in function, they are both cast to `Real`.</span></span>

1. <span data-ttu-id="d5ee8-188">建立 `DatabaseSource` 以連接到資料庫並執行查詢。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-188">Create a `DatabaseSource` to connect to the database and execute the query.</span></span>

    [!code-csharp [CreateDBSource](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L27-L29)]

1. <span data-ttu-id="d5ee8-189">將資料載入 `IDataView`。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-189">Load the data into an `IDataView`.</span></span>

    [!code-csharp [LoadData](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L31)]

1. <span data-ttu-id="d5ee8-190">此資料集包含兩年的資料。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-190">The dataset contains two years worth of data.</span></span> <span data-ttu-id="d5ee8-191">只有第一年的資料會用於定型，第二年則是用來比較實際值與模型產生的預測。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-191">Only data from the first year is used for training, the second year is held out to compare the actual values against the forecast produced by the model.</span></span> <span data-ttu-id="d5ee8-192">使用[`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*)轉換來篩選資料。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-192">Filter the data using the [`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) transform.</span></span> 

    [!code-csharp [SplitData](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L33-L34)]

    <span data-ttu-id="d5ee8-193">在第一年中，只有 `Year` 資料行中小於1的值，是藉由將 `upperBound` 參數設定為1來選取。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-193">For the first year, only the values in the `Year` column less than 1 are selected by setting the `upperBound` parameter to 1.</span></span> <span data-ttu-id="d5ee8-194">相反地，在第二個年份中，會選取大於或等於1的值，方法是將 `lowerBound` 參數設定為1。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-194">Conversely, for the second year, values greater than or equal to 1 are selected by setting the `lowerBound` parameter to 1.</span></span>

## <a name="define-time-series-analysis-pipeline"></a><span data-ttu-id="d5ee8-195">定義時間序列分析管線</span><span class="sxs-lookup"><span data-stu-id="d5ee8-195">Define time series analysis pipeline</span></span>

1. <span data-ttu-id="d5ee8-196">定義管線，以使用[SsaForecastingEstimator](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator)來預測時間序列資料集中的值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-196">Define a pipeline that uses the [SsaForecastingEstimator](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator) to forecast values in a time-series dataset.</span></span>

    [!code-csharp [DefinePipeline](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L36-L45)]

    <span data-ttu-id="d5ee8-197">`forecastingPipeline` 會在第一年取得365資料點，並取樣，或將時間序列資料集分割成 `seriesLength` 參數所指定的30天（每月）間隔。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-197">The `forecastingPipeline` takes 365 data points for the first year and samples or splits the time-series dataset into 30-day (monthly) intervals as specified by the `seriesLength` parameter.</span></span> <span data-ttu-id="d5ee8-198">每個範例都是透過每週或7天的時段進行分析。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-198">Each of these samples is analyzed through weekly or a 7-day window.</span></span> <span data-ttu-id="d5ee8-199">在判斷下一個期間的預測值為何時，會使用過去七天的值進行預測。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-199">When determining what the forecasted value for the next period(s) is, the values from previous seven days are used to make a prediction.</span></span> <span data-ttu-id="d5ee8-200">此模型設定為以 `horizon` 參數定義的未來預測七個週期。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-200">The model is set to forecast seven periods into the future as defined by the `horizon` parameter.</span></span> <span data-ttu-id="d5ee8-201">由於預測是一種明智的猜測，因此不一定總是100% 精確。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-201">Because a forecast is an informed guess, it's not always 100% accurate.</span></span> <span data-ttu-id="d5ee8-202">因此，最好能在最佳和最糟的案例中，根據上限和下限所定義的值範圍來瞭解。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-202">Therefore, it's good to know the range of values in the best and worst-case scenarios as defined by the upper and lower bounds.</span></span> <span data-ttu-id="d5ee8-203">在此情況下，較低和上限的信心層級會設定為95%。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-203">In this case, the level of confidence for the lower and upper bounds is set to 95%.</span></span> <span data-ttu-id="d5ee8-204">信賴等級可以相應增加或減少。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-204">The confidence level can be increased or decreased accordingly.</span></span> <span data-ttu-id="d5ee8-205">值愈高，範圍的寬度就會介於上限和下限之間，以達到所需的信心層級。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-205">The higher the value, the wider the range is between the upper and lower bounds to achieve the desired level of confidence.</span></span> 

1. <span data-ttu-id="d5ee8-206">使用[`Fit`](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator.Fit*)方法來定型模型，並將資料符合先前定義的 `forecastingPipeline`。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-206">Use the [`Fit`](xref:Microsoft.ML.Transforms.TimeSeries.SsaForecastingEstimator.Fit*) method to train the model and fit the data to the previously defined `forecastingPipeline`.</span></span>

    [!code-csharp [TrainModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L47)]

## <a name="evaluate-the-model"></a><span data-ttu-id="d5ee8-207">評估模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-207">Evaluate the model</span></span>

<span data-ttu-id="d5ee8-208">藉由預測下一年的資料，並將其與實際值進行比較，來評估模型的執行程度。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-208">Evaluate how well the model performs by forecasting next year's data and comparing it against the actual values.</span></span>

1. <span data-ttu-id="d5ee8-209">在 `Main` 方法底下，建立稱為 `Evaluate`的新公用程式方法。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-209">Below the `Main` method, create a new utility method called `Evaluate`.</span></span>

    ```csharp
    static void Evaluate(IDataView testData, ITransformer model, MLContext mlContext)
    {
        
    }
    ```

1. <span data-ttu-id="d5ee8-210">在 `Evaluate` 方法中，使用[`Transform`](xref:Microsoft.ML.ITransformer.Transform*)方法搭配定型的模型，以預測第二年的資料。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-210">Inside the `Evaluate` method, forecast the second year's data by using the [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) method with the trained model.</span></span>

    [!code-csharp [EvaluateForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L62)]

1. <span data-ttu-id="d5ee8-211">使用[`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*)方法，從資料取得實際的值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-211">Get the actual values from the data by using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method.</span></span>

    [!code-csharp [GetActualRentals](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L65-L67)]

1. <span data-ttu-id="d5ee8-212">使用[`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*)方法取得預測值。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-212">Get the forecast values by using the [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) method.</span></span>

    [!code-csharp [GetForecastRentals](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L70-L72)]

1. <span data-ttu-id="d5ee8-213">計算實際和預測值之間的差異，通常稱為「錯誤」。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-213">Calculate the difference between the actual and forecast values, commonly referred to as the error.</span></span>

    [!code-csharp [CalculateError](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L75)]

1. <span data-ttu-id="d5ee8-214">藉由計算平均絕對錯誤和根 Mean 平方誤差值來測量效能。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-214">Measure performance by computing the Mean Absolute Error and Root Mean Squared Error values.</span></span>

    [!code-csharp [CalculateMetrics](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L78-L79)]

    <span data-ttu-id="d5ee8-215">若要評估效能，會使用下列計量：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-215">To evaluate performance, the following metrics are used:</span></span>

    - <span data-ttu-id="d5ee8-216">**平均絕對錯誤**：測量接近預測與實際值的方式。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-216">**Mean Absolute Error**: Measures how close predictions are to the actual value.</span></span> <span data-ttu-id="d5ee8-217">這個值的範圍介於0與無限大之間。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-217">This value ranges between 0 and infinity.</span></span> <span data-ttu-id="d5ee8-218">愈接近0，模型的品質愈好。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-218">The closer to 0, the better the quality of the model.</span></span>
    - <span data-ttu-id="d5ee8-219">**根平均平方誤差**：摘要說明模型中的憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-219">**Root Mean Squared Error**: Summarizes thhe error in the model.</span></span> <span data-ttu-id="d5ee8-220">這個值的範圍介於0與無限大之間。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-220">This value ranges between 0 and infinity.</span></span> <span data-ttu-id="d5ee8-221">愈接近0，模型的品質愈好。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-221">The closer to 0, the better the quality of the model.</span></span>

1. <span data-ttu-id="d5ee8-222">將計量輸出至主控台。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-222">Output the metrics to the console.</span></span>

    [!code-csharp [OutputMetrics](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L82-L85)]

1. <span data-ttu-id="d5ee8-223">使用 `Main` 方法內的 `Evaluate` 方法。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-223">Use the `Evaluate` method inside the `Main` method.</span></span>

    [!code-csharp [EvaluateModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L49)]

## <a name="save-the-model"></a><span data-ttu-id="d5ee8-224">儲存模型</span><span class="sxs-lookup"><span data-stu-id="d5ee8-224">Save the model</span></span>

<span data-ttu-id="d5ee8-225">如果您對模型感到滿意，請儲存以供稍後在其他應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-225">If you're satisfied with your model, save it for later use in other applications.</span></span>

1. <span data-ttu-id="d5ee8-226">在 `Main` 方法中，建立[`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602)。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-226">In the `Main` method, create a [`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602).</span></span> <span data-ttu-id="d5ee8-227">[`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602)是進行單一預測的便利方法。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-227">[`TimeSeriesPredictionEngine`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602) is a convenience method to make single predictions.</span></span>

    [!code-csharp [CreateTimeSeriesEngine](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L51)]

1. <span data-ttu-id="d5ee8-228">將模型儲存至名為 `MLModel.zip` 的檔案，如先前定義的 `modelPath` 變數所指定。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-228">Save the model to a file called `MLModel.zip` as specified by the previously defined `modelPath` variable.</span></span> <span data-ttu-id="d5ee8-229">使用[`Checkpoint`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.CheckPoint*)方法來儲存模型。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-229">Use the [`Checkpoint`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.CheckPoint*) method to save the model.</span></span>

    [!code-csharp [SaveModel](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L52)]

## <a name="use-the-model-to-forecast-demand"></a><span data-ttu-id="d5ee8-230">使用模型來預測需求</span><span class="sxs-lookup"><span data-stu-id="d5ee8-230">Use the model to forecast demand</span></span>

1. <span data-ttu-id="d5ee8-231">在 `Evaluate` 方法底下，建立稱為 `Forecast`的新公用程式方法。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-231">Below the `Evaluate` method, create a new utility method called `Forecast`.</span></span>

    ```csharp
    static void Forecast(IDataView testData, int horizon, TimeSeriesPredictionEngine<ModelInput, ModelOutput> forecaster, MLContext mlContext)
    {

    }
    ```

1. <span data-ttu-id="d5ee8-232">在 `Forecast` 方法中，使用[`Predict`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.Predict*)方法來預測接下來七天的租用。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-232">Inside the `Forecast` method, use the [`Predict`](xref:Microsoft.ML.Transforms.TimeSeries.TimeSeriesPredictionEngine%602.Predict*) method to forecast rentals for the next seven days.</span></span>

    [!code-csharp [SingleForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L91)]

1. <span data-ttu-id="d5ee8-233">將 [實際] 和 [預測] 值對齊七個期間。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-233">Align the actual and forecast values for seven periods.</span></span>

    [!code-csharp [GetForecastOutput](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L93-L108)]

1. <span data-ttu-id="d5ee8-234">逐一查看預測輸出，並將它顯示在主控台上。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-234">Iterate through the forecast output and display it on the console.</span></span>

    [!code-csharp [DisplayForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L111-L116)]

## <a name="run-the-application"></a><span data-ttu-id="d5ee8-235">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d5ee8-235">Run the application</span></span>

1. <span data-ttu-id="d5ee8-236">在 `Main` 方法中，呼叫 `Forecast` 方法。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-236">Inside the `Main` method, call the `Forecast` method.</span></span>

    [!code-csharp [BuildForecast](~/machinelearning-samples/samples/csharp/getting-started/Forecasting_BikeSharingDemand/BikeDemandForecasting/Program.cs#L54)]

1. <span data-ttu-id="d5ee8-237">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-237">Run the application.</span></span> <span data-ttu-id="d5ee8-238">與下面類似的輸出應該會出現在主控台上。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-238">Output similar to that below should appear on the console.</span></span> <span data-ttu-id="d5ee8-239">為求簡潔，輸出已壓縮。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-239">For brevity, the output has been condensed.</span></span>

    ```text
    Evaluation Metrics
    ---------------------
    Mean Absolute Error: 726.416
    Root Mean Squared Error: 987.658

    Rental Forecast
    ---------------------
    Date: 1/1/2012
    Actual Rentals: 2294
    Lower Estimate: 1197.842
    Forecast: 2334.443
    Upper Estimate: 3471.044

    Date: 1/2/2012
    Actual Rentals: 1951
    Lower Estimate: 1148.412
    Forecast: 2360.861
    Upper Estimate: 3573.309
    ```

<span data-ttu-id="d5ee8-240">檢查實際和預測的值，會顯示下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="d5ee8-240">Inspection of the actual and forecasted values shows the following relationships:</span></span>

![實際與預測比較](./media/time-series-demand-forecasting/forecast.png)

<span data-ttu-id="d5ee8-242">雖然預測的值不會預測確切的租用數目，但它們提供的值範圍較窄，可讓作業優化資源的使用。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-242">While the forecasted values are not predicting the exact number of rentals, they provide a more narrow range of values that allows an operation to optimize their use of resources.</span></span> 

<span data-ttu-id="d5ee8-243">恭喜您！</span><span class="sxs-lookup"><span data-stu-id="d5ee8-243">Congratulations!</span></span> <span data-ttu-id="d5ee8-244">您現在已成功建立時間序列機器學習模型來預測自行車出租需求。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-244">You've now successfully built a time series machine learning model to forecast bike rental demand.</span></span>

<span data-ttu-id="d5ee8-245">您可以在[dotnet/machinelearning 範例](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand)存放庫中找到本教學課程的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="d5ee8-245">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/Forecasting_BikeSharingDemand) repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5ee8-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5ee8-246">Next steps</span></span>

- [<span data-ttu-id="d5ee8-247">ML.NET 中的機器學習工作</span><span class="sxs-lookup"><span data-stu-id="d5ee8-247">Machine learning tasks in ML.NET</span></span>](../resources/tasks.md)
- [<span data-ttu-id="d5ee8-248">改善模型精確度</span><span class="sxs-lookup"><span data-stu-id="d5ee8-248">Improve model accuracy</span></span>](../resources/improve-machine-learning-model-ml-net.md)