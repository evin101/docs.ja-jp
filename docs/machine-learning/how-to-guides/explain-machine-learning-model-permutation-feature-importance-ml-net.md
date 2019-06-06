---
title: Permutation Feature Importance を使用したモデル予測の説明
description: ML.NET の Permutation Feature Importance を使ってモデルの特徴の重要度を理解する
ms.date: 05/02/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: 51ef4b55b1518381881e57d83fd43f8ec7f786c6
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645059"
---
# <a name="explain-model-predictions-using-permutation-feature-importance"></a><span data-ttu-id="94781-103">Permutation Feature Importance を使用してモデル予測を説明する</span><span class="sxs-lookup"><span data-stu-id="94781-103">Explain model predictions using Permutation Feature Importance</span></span>

<span data-ttu-id="94781-104">Permutation Feature Importance (PFI) を使用した予測に対する特徴のコントリビューションを理解して、ML.NET の機械学習モデル予測を説明する方法について学習します。</span><span class="sxs-lookup"><span data-stu-id="94781-104">Learn how to explain ML.NET machine learning model predictions by understanding the contribution features have to predictions using Permutation Feature Importance (PFI).</span></span>

<span data-ttu-id="94781-105">機械学習モデルは、入力を受け取り、出力を生成するブラック ボックスと考えられることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="94781-105">Machine learning models are often thought of as black boxes that take inputs and generate an output.</span></span> <span data-ttu-id="94781-106">出力に影響する中間手順や特徴間の相互作用は、あまり理解されていません。</span><span class="sxs-lookup"><span data-stu-id="94781-106">The intermediate steps or interactions among the features that influence the output are rarely understood.</span></span> <span data-ttu-id="94781-107">医療など、日常生活の多くの側面に機械学習が導入されるにつれて、機械学習モデルが決定を下す理由を理解することの重要度が最も高くなりました。</span><span class="sxs-lookup"><span data-stu-id="94781-107">As machine learning is introduced into more aspects of everyday life such as healthcare, it's of utmost importance to understand why a machine learning model makes the decisions it does.</span></span> <span data-ttu-id="94781-108">たとえば、機械学習モデルによって診断が行われる場合、医療従事者には、その診断が下された要因を調べる方法が必要です。</span><span class="sxs-lookup"><span data-stu-id="94781-108">For example, if diagnoses are made by a machine learning model, healthcare professionals need a way to look into the factors that went into making that diagnoses.</span></span> <span data-ttu-id="94781-109">適切な診断を提供することは、患者が迅速に回復するかどうかに大きな違いをもたらす可能性があります。</span><span class="sxs-lookup"><span data-stu-id="94781-109">Providing the right diagnosis could make a great difference on whether a patient has a speedy recovery or not.</span></span> <span data-ttu-id="94781-110">そのため、モデル内の説明可能性のレベルが高いほど、モデルによって行われた決定を医療従事者が承認または拒否する必要がある場合の信頼性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="94781-110">Therefore the higher the level of explainability in a model, the greater confidence healthcare professionals have to accept or reject the decisions made by the model.</span></span>

<span data-ttu-id="94781-111">モデルの説明にはさまざまな手法が使用されており、その 1 つに PFI があります。</span><span class="sxs-lookup"><span data-stu-id="94781-111">Various techniques are used to explain models, one of which is PFI.</span></span> <span data-ttu-id="94781-112">PFI は、[Breiman の「*Random Forests (ランダム フォレスト)* 」論文](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf) (セクション 10 を参照してください) にインスパイアされた、分類および回帰モデルの説明に使用される手法です。</span><span class="sxs-lookup"><span data-stu-id="94781-112">PFI is a technique used to explain classification and regression models that is inspired by [Breiman's *Random Forests* paper](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)(see section 10).</span></span> <span data-ttu-id="94781-113">概要を説明すると、データセット全体に対して一度に 1 つの特徴のデータをランダムにシャッフルし、関心のあるパフォーマンス メトリックがどのくらい低下するかを計算するしくみです。</span><span class="sxs-lookup"><span data-stu-id="94781-113">At a high level, the way it works is by randomly shuffling data one feature at a time for the entire dataset and calculating how much the performance metric of interest decreases.</span></span> <span data-ttu-id="94781-114">変更が大きいほど、その特徴の重要度は高くなります。</span><span class="sxs-lookup"><span data-stu-id="94781-114">The larger the change, the more important that feature is.</span></span> 

<span data-ttu-id="94781-115">さらに、最も重要な特徴を強調することで、モデル作成者はより重要な特徴のサブセットの使用に集中し、ノイズとトレーニング時間を減らすことができるようになります。</span><span class="sxs-lookup"><span data-stu-id="94781-115">Additionally, by highlighting the most important features, model builders can focus on using a subset of more meaningful features which can potentially reduce noise and training time.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="94781-116">データを読み込む</span><span class="sxs-lookup"><span data-stu-id="94781-116">Load the data</span></span>

<span data-ttu-id="94781-117">このサンプルに使用されているデータセットの特徴は、1 - 12 列目にあります。</span><span class="sxs-lookup"><span data-stu-id="94781-117">The features in the dataset being used for this sample are in columns 1-12.</span></span> <span data-ttu-id="94781-118">目標は `Price` を予測することです。</span><span class="sxs-lookup"><span data-stu-id="94781-118">The goal is to predict `Price`.</span></span> 

| <span data-ttu-id="94781-119">Column</span><span class="sxs-lookup"><span data-stu-id="94781-119">Column</span></span> | <span data-ttu-id="94781-120">機能</span><span class="sxs-lookup"><span data-stu-id="94781-120">Feature</span></span> | <span data-ttu-id="94781-121">説明</span><span class="sxs-lookup"><span data-stu-id="94781-121">Description</span></span> 
| --- | --- | --- |
| <span data-ttu-id="94781-122">1</span><span class="sxs-lookup"><span data-stu-id="94781-122">1</span></span> | <span data-ttu-id="94781-123">CrimeRate</span><span class="sxs-lookup"><span data-stu-id="94781-123">CrimeRate</span></span> | <span data-ttu-id="94781-124">1 人当たりの犯罪率</span><span class="sxs-lookup"><span data-stu-id="94781-124">Per capita crime rate</span></span>
| <span data-ttu-id="94781-125">2</span><span class="sxs-lookup"><span data-stu-id="94781-125">2</span></span> | <span data-ttu-id="94781-126">ResidentialZones</span><span class="sxs-lookup"><span data-stu-id="94781-126">ResidentialZones</span></span> | <span data-ttu-id="94781-127">町の住宅地区</span><span class="sxs-lookup"><span data-stu-id="94781-127">Residential zones in town</span></span>
| <span data-ttu-id="94781-128">3</span><span class="sxs-lookup"><span data-stu-id="94781-128">3</span></span> | <span data-ttu-id="94781-129">CommercialZones</span><span class="sxs-lookup"><span data-stu-id="94781-129">CommercialZones</span></span> | <span data-ttu-id="94781-130">町の非住宅地区</span><span class="sxs-lookup"><span data-stu-id="94781-130">Non-residential zones in town</span></span>
| <span data-ttu-id="94781-131">4</span><span class="sxs-lookup"><span data-stu-id="94781-131">4</span></span> | <span data-ttu-id="94781-132">NearWater</span><span class="sxs-lookup"><span data-stu-id="94781-132">NearWater</span></span> | <span data-ttu-id="94781-133">水域への近さ</span><span class="sxs-lookup"><span data-stu-id="94781-133">Proximity to body of water</span></span>
| <span data-ttu-id="94781-134">5</span><span class="sxs-lookup"><span data-stu-id="94781-134">5</span></span> | <span data-ttu-id="94781-135">ToxicWasteLevels</span><span class="sxs-lookup"><span data-stu-id="94781-135">ToxicWasteLevels</span></span> | <span data-ttu-id="94781-136">毒性レベル (PPM)</span><span class="sxs-lookup"><span data-stu-id="94781-136">Toxicity levels (PPM)</span></span>
| <span data-ttu-id="94781-137">6</span><span class="sxs-lookup"><span data-stu-id="94781-137">6</span></span> | <span data-ttu-id="94781-138">AverageRoomNumber</span><span class="sxs-lookup"><span data-stu-id="94781-138">AverageRoomNumber</span></span> | <span data-ttu-id="94781-139">住宅内の平均部屋数</span><span class="sxs-lookup"><span data-stu-id="94781-139">Average number of rooms in house</span></span>
| <span data-ttu-id="94781-140">7</span><span class="sxs-lookup"><span data-stu-id="94781-140">7</span></span> | <span data-ttu-id="94781-141">HomeAge</span><span class="sxs-lookup"><span data-stu-id="94781-141">HomeAge</span></span> | <span data-ttu-id="94781-142">住宅の築年数</span><span class="sxs-lookup"><span data-stu-id="94781-142">Age of home</span></span>
| <span data-ttu-id="94781-143">8</span><span class="sxs-lookup"><span data-stu-id="94781-143">8</span></span> | <span data-ttu-id="94781-144">BusinessCenterDistance</span><span class="sxs-lookup"><span data-stu-id="94781-144">BusinessCenterDistance</span></span> | <span data-ttu-id="94781-145">最寄りのビジネス地区までの距離</span><span class="sxs-lookup"><span data-stu-id="94781-145">Distance to nearest business district</span></span>
| <span data-ttu-id="94781-146">9</span><span class="sxs-lookup"><span data-stu-id="94781-146">9</span></span> | <span data-ttu-id="94781-147">HighwayAccess</span><span class="sxs-lookup"><span data-stu-id="94781-147">HighwayAccess</span></span> | <span data-ttu-id="94781-148">幹線道路までの近さ</span><span class="sxs-lookup"><span data-stu-id="94781-148">Proximity to highways</span></span>
| <span data-ttu-id="94781-149">10</span><span class="sxs-lookup"><span data-stu-id="94781-149">10</span></span> | <span data-ttu-id="94781-150">TaxRate</span><span class="sxs-lookup"><span data-stu-id="94781-150">TaxRate</span></span> | <span data-ttu-id="94781-151">固定資産税率</span><span class="sxs-lookup"><span data-stu-id="94781-151">Property tax rate</span></span>
| <span data-ttu-id="94781-152">11</span><span class="sxs-lookup"><span data-stu-id="94781-152">11</span></span> | <span data-ttu-id="94781-153">StudentTeacherRatio</span><span class="sxs-lookup"><span data-stu-id="94781-153">StudentTeacherRatio</span></span> | <span data-ttu-id="94781-154">教師に対する学生の比率</span><span class="sxs-lookup"><span data-stu-id="94781-154">Ratio of students to teachers</span></span>
| <span data-ttu-id="94781-155">12</span><span class="sxs-lookup"><span data-stu-id="94781-155">12</span></span> | <span data-ttu-id="94781-156">PercentPopulationBelowPoverty</span><span class="sxs-lookup"><span data-stu-id="94781-156">PercentPopulationBelowPoverty</span></span> | <span data-ttu-id="94781-157">貧困を下回る生活を送っている人口の割合</span><span class="sxs-lookup"><span data-stu-id="94781-157">Percent of population living below poverty</span></span>
| <span data-ttu-id="94781-158">13</span><span class="sxs-lookup"><span data-stu-id="94781-158">13</span></span> | <span data-ttu-id="94781-159">Price</span><span class="sxs-lookup"><span data-stu-id="94781-159">Price</span></span> | <span data-ttu-id="94781-160">住宅の価格</span><span class="sxs-lookup"><span data-stu-id="94781-160">Price of the home</span></span>

<span data-ttu-id="94781-161">データセットの例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="94781-161">A sample of the dataset is shown below:</span></span>

```text
1,24,13,1,0.59,3,96,11,23,608,14,13,32
4,80,18,1,0.37,5,14,7,4,346,19,13,41
2,98,16,1,0.25,10,5,1,8,689,13,36,12
```

<span data-ttu-id="94781-162">このサンプルのデータは、`HousingPriceData` のようなクラスでモデル化できます。</span><span class="sxs-lookup"><span data-stu-id="94781-162">The data in this sample can be modeled by a class like `HousingPriceData`:</span></span>

```csharp
class HousingPriceData
{
    [LoadColumn(0)]
    public float CrimeRate { get; set; }

    [LoadColumn(1)]
    public float ResidentialZones { get; set; }

    [LoadColumn(2)]
    public float CommercialZones { get; set; }

    [LoadColumn(3)]
    public float NearWater { get; set; }

    [LoadColumn(4)]
    public float ToxicWasteLevels { get; set; }

    [LoadColumn(5)]
    public float AverageRoomNumber { get; set; }

    [LoadColumn(6)]
    public float HomeAge { get; set; }

    [LoadColumn(7)]
    public float BusinessCenterDistance { get; set; }

    [LoadColumn(8)]
    public float HighwayAccess { get; set; }

    [LoadColumn(9)]
    public float TaxRate { get; set; }

    [LoadColumn(10)]
    public float StudentTeacherRatio { get; set; }

    [LoadColumn(11)]
    public float PercentPopulationBelowPoverty { get; set; }

    [LoadColumn(12)]
    [ColumnName("Label")]
    public float Price { get; set; }
}
```

<span data-ttu-id="94781-163">データを [`IDataView`](xref:Microsoft.ML.IDataView) に読み込みます。</span><span class="sxs-lookup"><span data-stu-id="94781-163">Load the data into an [`IDataView`](xref:Microsoft.ML.IDataView).</span></span>

## <a name="train-the-model"></a><span data-ttu-id="94781-164">モデルをトレーニングする</span><span class="sxs-lookup"><span data-stu-id="94781-164">Train the model</span></span>

<span data-ttu-id="94781-165">次のコード サンプルは、線形回帰モデルをトレーニングして住宅価格を予測するプロセスを示しています。</span><span class="sxs-lookup"><span data-stu-id="94781-165">The code sample below illustrates the process of training a linear regression model to predict house prices.</span></span>

```csharp
// 1. Get the column name of input features.
string[] featureColumnNames = 
    data.Schema
        .Select(column => column.Name)
        .Where(columnName => columnName != "Label").ToArray();

// 2. Define estimator with data pre-processing steps
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", featureColumnNames)
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// 3. Create transformer using the data pre-processing estimator
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// 4. Pre-process the training data
IDataView preprocessedTrainData = dataPrepTransformer.Transform(data);

// 5. Define Stochastic Dual Coordinate Ascent machine learning estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// 6. Train machine learning model
var sdcaModel = sdcaEstimator.Fit(preprocessedTrainData);
```

## <a name="explain-the-model-with-permutation-feature-importance-pfi"></a><span data-ttu-id="94781-166">Permutation Feature Importance (PFI) を使用してモデルを説明する</span><span class="sxs-lookup"><span data-stu-id="94781-166">Explain the model with Permutation Feature Importance (PFI)</span></span>

<span data-ttu-id="94781-167">ML.NET では、それぞれのタスクに [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="94781-167">In ML.NET use the [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) method for your respective task.</span></span>

```csharp
ImmutableArray<RegressionMetricsStatistics> permutationFeatureImportance = 
    mlContext
        .Regression
        .PermutationFeatureImportance(sdcaModel, preprocessedTrainData, permutationCount:3);
```

<span data-ttu-id="94781-168">トレーニング データセットに対して [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) を使用した結果は、[`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) オブジェクトの [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray) になります。</span><span class="sxs-lookup"><span data-stu-id="94781-168">The result of using [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) on the training dataset is an [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray) of [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) objects.</span></span> <span data-ttu-id="94781-169">[`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) は、`permutationCount` パラメーターに指定された順列の数と等しい [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics)の複数の観測値について、平均や標準偏差などの概要の統計情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="94781-169">[`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) provides summary statistics like mean and standard deviation for multiple observations of [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) equal to the number of permutations specified by the `permutationCount` parameter.</span></span>

<span data-ttu-id="94781-170">重要度、このケースで言い換えると、[`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) によって計算される R-2 乗メトリックの絶対平均減少は、最も高い重要度から最も低い重要度の順に並べ替えることができます。</span><span class="sxs-lookup"><span data-stu-id="94781-170">The importance, or in this case, the absolute average decrease in R-squared metric calculated by [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) can then be ordered from most important to least important.</span></span>  

```csharp
// Order features by importance
var featureImportanceMetrics =
    permutationFeatureImportance
        .Select((metric, index) => new { index, metric.RSquared })
        .OrderByDescending(myFeatures => Math.Abs(myFeatures.RSquared.Mean));

Console.WriteLine("Feature\tPFI");

foreach (var feature in featureImportanceMetrics)
{
    Console.WriteLine($"{featureColumnNames[feature.index],-20}|\t{feature.RSquared.Mean:F6}");
}
```

<span data-ttu-id="94781-171">`featureImportanceMetrics` の各特徴の値を出力すると、以下のような出力が生成されます。</span><span class="sxs-lookup"><span data-stu-id="94781-171">Printing the values for each of the features in `featureImportanceMetrics` would generate output similar to that below.</span></span> <span data-ttu-id="94781-172">これらの値は指定されたデータに基づいて変わるため、異なる結果が表示されることを想定する点に注意してください。</span><span class="sxs-lookup"><span data-stu-id="94781-172">Keep in mind that you should expect to see different results because these values vary based on the data that they are given.</span></span>  

| <span data-ttu-id="94781-173">機能</span><span class="sxs-lookup"><span data-stu-id="94781-173">Feature</span></span> | <span data-ttu-id="94781-174">R-2 乗に変更</span><span class="sxs-lookup"><span data-stu-id="94781-174">Change to R-Squared</span></span> |
|:--|:--:|
<span data-ttu-id="94781-175">HighwayAccess</span><span class="sxs-lookup"><span data-stu-id="94781-175">HighwayAccess</span></span>       |   <span data-ttu-id="94781-176">-0.042731</span><span class="sxs-lookup"><span data-stu-id="94781-176">-0.042731</span></span>
<span data-ttu-id="94781-177">StudentTeacherRatio</span><span class="sxs-lookup"><span data-stu-id="94781-177">StudentTeacherRatio</span></span> |   <span data-ttu-id="94781-178">-0.012730</span><span class="sxs-lookup"><span data-stu-id="94781-178">-0.012730</span></span>
<span data-ttu-id="94781-179">BusinessCenterDistance</span><span class="sxs-lookup"><span data-stu-id="94781-179">BusinessCenterDistance</span></span>| <span data-ttu-id="94781-180">-0.010491</span><span class="sxs-lookup"><span data-stu-id="94781-180">-0.010491</span></span>
<span data-ttu-id="94781-181">TaxRate</span><span class="sxs-lookup"><span data-stu-id="94781-181">TaxRate</span></span>             |   <span data-ttu-id="94781-182">-0.008545</span><span class="sxs-lookup"><span data-stu-id="94781-182">-0.008545</span></span>
<span data-ttu-id="94781-183">AverageRoomNumber</span><span class="sxs-lookup"><span data-stu-id="94781-183">AverageRoomNumber</span></span>   |   <span data-ttu-id="94781-184">-0.003949</span><span class="sxs-lookup"><span data-stu-id="94781-184">-0.003949</span></span>
<span data-ttu-id="94781-185">CrimeRate</span><span class="sxs-lookup"><span data-stu-id="94781-185">CrimeRate</span></span>           |   <span data-ttu-id="94781-186">-0.003665</span><span class="sxs-lookup"><span data-stu-id="94781-186">-0.003665</span></span>
<span data-ttu-id="94781-187">CommercialZones</span><span class="sxs-lookup"><span data-stu-id="94781-187">CommercialZones</span></span>     |   <span data-ttu-id="94781-188">0.002749</span><span class="sxs-lookup"><span data-stu-id="94781-188">0.002749</span></span>
<span data-ttu-id="94781-189">HomeAge</span><span class="sxs-lookup"><span data-stu-id="94781-189">HomeAge</span></span>             |   <span data-ttu-id="94781-190">-0.002426</span><span class="sxs-lookup"><span data-stu-id="94781-190">-0.002426</span></span>
<span data-ttu-id="94781-191">ResidentialZones</span><span class="sxs-lookup"><span data-stu-id="94781-191">ResidentialZones</span></span>    |   <span data-ttu-id="94781-192">-0.002319</span><span class="sxs-lookup"><span data-stu-id="94781-192">-0.002319</span></span>
<span data-ttu-id="94781-193">NearWater</span><span class="sxs-lookup"><span data-stu-id="94781-193">NearWater</span></span>           |   <span data-ttu-id="94781-194">0.000203</span><span class="sxs-lookup"><span data-stu-id="94781-194">0.000203</span></span>
<span data-ttu-id="94781-195">PercentPopulationLivingBelowPoverty</span><span class="sxs-lookup"><span data-stu-id="94781-195">PercentPopulationLivingBelowPoverty</span></span>|    <span data-ttu-id="94781-196">0.000031</span><span class="sxs-lookup"><span data-stu-id="94781-196">0.000031</span></span>
<span data-ttu-id="94781-197">ToxicWasteLevels</span><span class="sxs-lookup"><span data-stu-id="94781-197">ToxicWasteLevels</span></span>    |   <span data-ttu-id="94781-198">-0.000019</span><span class="sxs-lookup"><span data-stu-id="94781-198">-0.000019</span></span>

<span data-ttu-id="94781-199">このデータセットの重要度が高い特徴の上位 5 つを見ると、このモデルによって予測される住宅の価格は、幹線道路までの近さ、その地域の学校の学生と教師の比率、主要な雇用中心地への近さ、固定資産税率、住宅内の平均部屋数の影響を受けます。</span><span class="sxs-lookup"><span data-stu-id="94781-199">Taking a look at the the five most important features for this dataset, the price of a house predicted by this model is influenced by its proximity to highways, student teacher ratio of schools in the area, proximity to major employment centers, property tax rate and average number of rooms in the home.</span></span>