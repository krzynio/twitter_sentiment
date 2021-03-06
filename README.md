# Analysis of Twitter sentiment with various Language Models on narrow-scope data
This repository contains data, code and results for fine-grained sentiment analysis. The paper describing this research is in preparation.

*"Analysis of sentiment in tweets: comparison of model performance and explainability of predictions"*

Authors: Krzysztof Fiok1, Waldemar Karwowski1, Edgar Gutierrez-Franco1, and Maciej Wilamowski2


1 University of Central Florida, Department of Industrial Engineering & Management Systems, Orlando, Florida, USA </br>
2 University of Warsaw, Faculty of Economic Sciences, Warsaw, Poland
<br/>


The whole repository is published under MIT License (please refer to the [License file](https://github.com/krzysztoffiok/twitter_sentiment/blob/master/LICENSE)).

In due course full description of usage will appear here.

The code is written in Python3 and requires GPU computing machine for achieving reasonable performance.

## Preliminary results

  |   |   |   |   | Flair | Flair | Flair | Flair | Flair
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
  |   |   |   |   | Pooled | Pooled | biLSTM | biLSTM | CLS
Metric | Model | Term Frequency | LIWC | USE | FastText | RoBERTa | FastText | RoBERTa | RoBERTa
MCC | RF | 0.356 | 0.425 | 0.461 | 0.421 | 0.449 | 0.524 | 0.594 | 0.609
MCC | XGB | 0.465 | 0.466 | 0.537 | 0.48 | 0.541 | 0.527 | 0.586 | 0.613
F1 | RF | 0.498 | 0.596 | 0.582 | 0.557 | 0.579 | 0.665 | 0.721 | 0.732
F1 | XGB | 0.615 | 0.628 | 0.672 | 0.63 | 0.678 | 0.673 | 0.719 | 0.736


Abbrevations stand for:</br>
RF: sklearn.ensemble.RandomForestClassifier(n_estimators=250, max_depth=7, min_samples_split=2, min_samples_leaf=1, max_features='auto', n_jobs=-1, random_state=2020)</br>
XGB: xgb.XGBClassifier(objective='multi:softprob', n_jobs=24, learning_rate=0.03,
max_depth=10, subsample=0.7, colsample_bytree=0.6, random_state=2020, n_estimators=250)</br>
USE: Universal Sentence Encoder</br>
LIWC: Linguistic Enquiry and Word Count</br>
MCC: sklearn.metrics.matthews_corrcoef</br>
F1: sklearn.metrics.f1_score(average="weighted")</br>

## Try how it works in google colaboratory:

[Train your own Deep Learning Language Models or reproduce our results with Google colaboratory](https://colab.research.google.com/drive/1K-XQJnauYvULdwUO3vELy9dJ1DHR_53b) </br>
Select the runtime type Python3 with GPU acceleration for reasonable performance if you wish to train you own Deep Learning Language Models or simple CPU runtime if you want to use embeddings computed in our work.

Important: in some cases due to Google Colaboratory GPU memory limitations training of all Deep Learning Language Models may not be possible.


## Installation if you wish to try our code locally:
Please clone this repository and extract zipped files downloaded from "release" section.

## How the code works:
You start with a labeled data set of 5000 tweets (file is completely anonymized). There are 5 sentiment classes (0-very negative, 1-negative, 2-neutral, 3-positive, 4-very positive).

PART I. Training Language Models and embedding tweet texts.
1) In order to carry out classification, you need to train Language Models on the provided data. Preparing 5-fold cross validated data splits is carried out in Google Colaboratory or if you run locally, in Flair_data_splitter.ipynb (jupyter notebook). It creates proper directories and files.
2) For training of Deep Learning Language Models(DLLMs) we utilize [Flair](https://github.com/flairNLP/flair). Again, this is carried out in Google Colaboratory or if you run locally you need to execute model_train.py according to instructions provided in the very same script. For this stage, GPU is definitely required.
3) After training DLLMs it is time to use them to convert tweet texts into vector representations (embeddings). This is carried out in Google Colaboratory or if you run locally you need to execute embed_sentences_flair.py according to instructions provided in the very same script. For this stage CPU is enough. Apart from models trained with Flair, we also create Universal Sentence Encoder embeddings which will run both with or without GPU.

PART II. Machine Learning over embedded tweets. </br>
Once the tweet texts are converted to embeddings Machine Learning classification can be carried out. Google Colaboratory can be used here as well or if you run locally please use tweet_sentiment.ipynb (jupyter notebook). Before the actuall Machine Learning classification is done we also compute vectors by means of simple Term Frequency modelling. In the repo we also provided Linguistic Inquiery and Word Count (LIWC) features computed for all analyzed tweets. Once the selected classification models are trained it is also possible to visualize explanations of model predictions which is carried out in the same scripts used to carry our Machine Learning classification.

It is possible to start from Part II and use embeddings computed for our paper. To do so either go to "Part II" section in Google Colaboratory notebook or if you run locally download embeddings from "release" section of this repository and use tweet_sentiment.ipynb file.

## Acknowledgment
This research was carried out as part of the N000141812559 ONR research grant.

## Citation:<br/>
If you decide to use here published code or our dataset please cite our work in the following manner:
(please contact us directly at this time since the paper is still in preparation).

