# Capstone Project

## Capstone Project Proposal - Network Traffic Anomaly Detection - Omar Sultan

### The research question you intend to answer:
Can I use ML-based classification techniques to reliably identify anomalous or potentially problematic network traffic?
**Note:** Becasue I ended up chnging out my dataset (see below), I adjusted the concept a bit to look at predicting future traffic trends

### Your expected data source(s):

*Note*

Working on this capstone also gave me some unplanned experence working through the first couple of steps of the CRISP-DM model. :)  I had some hiccups reconciling my concept and my training data:
1) I abandoned my orignal olan to use work from data, once I remembered that the dataset would be posted in a public GitHub Repo, that become a non-starter
2) The orginal Kaggel data sets I had considered  (https://www.kaggle.com/datasets/jsrojas/ip-network-traffic-flows-labeled-with-87-apps and https://www.kaggle.com/datasets/jsrojas/labeled-network-traffic-flows-114-applications) were not a good fit for the time series analysis I wanted to do--beter suited for a classifier
3) I did find a dataset that met my needs on the IEEE Dataport (https://ieee-dataport.org/documents/telecom-italia-and-opnet-datasets-network-traffic-prediction) but it was encode as a Matlib file and beyond my skills to extract
So...back to Kaggle

The dataset is from a Kaggle competition for time series forecasting for web traffic: https://www.kaggle.com/c/web-traffic-time-series-forecasting/overview
The training dataset consists of approximately 145k time series. Each of these time series represent a number of daily views of a different Wikipedia article, starting from July, 1st, 2015 up until September 10th, 2017. For the purposed of this project, I am only looking at the aggregate traffic, not the page-specific trends.

### The techniques you expect to use in your analysis

I expect to use the pretty strightforward time series analysis by looking for seaonsality, trying to establish whether the dataset is stationary then finally fitting a model.

### The expected results

I do expect to estblish trends in the data.  My real question is if the effort is worth the result--could I have gotten close enough with some simple linear regression.  For this project, the answer is maybe.  In real-life where I would be doing a more fine-grained multi-variate analysis, I think the answer is definitely in that scenario.

### Why this question is important

Data networks are central to every day life for both people and businesses so well operating networks are to everyone's benefit.  Most network operations tools are reactive in nature today (quickly identifying root cause analysis and possible resolutions).  Being able to proactively identify issues before they become noticeable and service impacting would be a huge benefit both to the companies that operate these networks and the employees and customers that use them.

## Data Exploration

<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/d5889acc-d21f-43b6-a222-41c0cacc384d">
The aggregate data is interesting in that it has a couple of changes in trend direction and some significant outliers.  The dark blue data is the training set and the light blue is the test set.


<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/5c0409b0-25d2-4301-9ecd-bd73989d8865">
The desnity plot shows a fairly Guassian distribution with the outlier visible in the raw data graph showing up at a smaller secondary bump.


<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/22d1df12-39dc-4fed-9c35-765137452421">
The boxplot is useful to start assessing the data with less noise and reveals a smoother trend than you migth expcect from the raw data.

<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/86d51b57-01c4-46a1-b6c9-f8ef6ea02853">
Looking a little deeper, there is no apparent seasonality to the data nor does there seem to be hidden struture in the residual.

<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/a254ba23-ba57-4769-832f-deae48f7eeaf">
Running the Augmented Dickey-Fuller Test yioled a p-vlaue of ~0.08 which is just over the threshold of 0.05, so, not stationary.

<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/91f267b5-ccae-48d2-af04-6cf5e0567bb5">
To be sure, looking at the rollng mean and rolling standard deviaion (STD).  While the STD is flat, the mean is not, so definitely not stationary.

## Modeling
Running through more analysis leads us to an Autoregressive Integrated Moving Average (ARIMA) model with parameters of:
- **p** (lag order) = 1
- **d** (degreee of diferenceing) = 0
- **q** (order of moving average) = 5

Fitting that model yields the following:
<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/bf1855b6-08b4-4fa9-aa34-41aef9bdebd6">

Running the test dataset through this model yiedls the following results:
<img width="999" alt="image" src="https://github.com/omarsultan/capstone/assets/6629296/28274ce0-8509-47db-8152-f1f03acf53a4">

## Results
For this test, I chose to go with MAPE as my metric for two reasons: 1) it is useful for time series forecasting, especially the speicifc network traffic I was looking at, and 2) I felt a % error was more useful than an aboslute number given the the large values of the underlyuing data we were dealing with and the dynamic eggs and flows of the traffic over time.  

The MAPE score for ths model was 3.66%.

## Next steps
1) I am sure there is plenty of room for optimizations so I would continue to refine and validate the model and approach.
2) I would explore this data using different, newer techniques such as using a reucrrent neural network like LSTM or perhaps one of the newer time series models like TimeGPT.




