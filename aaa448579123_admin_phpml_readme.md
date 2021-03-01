# phpml
基于PHP-ML库实现机器学习
### 基于语言学习
    基于语言学习，根据语言编码实现学习
### 实例
    require_once 'vendor/autoload.php';
    use Phpml\Classification\KNearestNeighbors; 
    use Phpml\Dataset\CsvDataset;
    use Phpml\Dataset\ArrayDataset;
    use Phpml\FeatureExtraction\TokenCountVectorizer;
    use Phpml\Tokenization\WordTokenizer;
    use Phpml\CrossValidation\StratifiedRandomSplit;
    use Phpml\FeatureExtraction\TfIdfTransformer;
    use Phpml\Metric\Accuracy;
    use Phpml\Classification\SVC;
    use Phpml\Regression\SVR;
    use Phpml\SupportVectorMachine\Kernel;

    $dataset = new CsvDataset('languages.csv', 1);
    $vectorizer = new TokenCountVectorizer(new WordTokenizer());
    $tfIdfTransformer = new TfIdfTransformer();

    $testample=['我是中国人'];


    $samples = [];
    foreach ($dataset->getSamples() as $sample) {
       $samples[] = $sample[0];
    }


    $vectorizer->fit($samples);
    $vectorizer->transform($samples);

    $vectorizer->fit($testample);
    $vectorizer->transform($testample);

    $tfIdfTransformer->fit($samples);
    $tfIdfTransformer->transform($samples);



    $dataset = new ArrayDataset($samples, $dataset->getTargets());

    $randomSplit = new StratifiedRandomSplit($dataset, 0.1);


    $classifier = new SVC(Kernel::RBF, 10000);
    $classifier->train($randomSplit->getTrainSamples(), $randomSplit->getTrainLabels());
    $testpredictedLabels = $classifier->predict($testample);

    print_r($testpredictedLabels);// return  Array ( [0] => zh )
    exit;
### 项目地址
    github：https://github.com/qieangel2013/phpml
      码云：https://gitee.com/qieangel2013/phpml



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)