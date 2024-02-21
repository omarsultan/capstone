# capstone

Capstone Project Proposal - Network Traffic Anomaly Detection - Omar Sultan
The research question you intend to answer:
Can I use ML-based classification techniques to reliably identify anomalous or potentially problematic network traffic?

Your expected data source(s):

I am working on securing a dataset of traffic from work.  If that does not work out, I have identified two potential datasets on Kaggle:

https://www.kaggle.com/datasets/jsrojas/ip-network-traffic-flows-labeled-with-87-appsLinks to an external site.
https://www.kaggle.com/datasets/jsrojas/labeled-network-traffic-flows-114-applicationsLinks to an external site.
The techniques you expect to use in your analysis

The nice thing about networking data is that it tends to be pretty complete and well labeled, so I don't expect to spend much time there.  I do expect to spend time on PCA and SFS to sift through the myriad features in a networking data set and also use tools like box plots to identify outliers, but, in this case is use them, not eliminate them.  In terms of modeling techniques, I am undecided, but I think either KNN or Decision Tress.  I think SVM might be useful too, but, TBH, I do not understand it well enough right now.  I expect to firm this up once i have gone through EDA.

The expected results

I do expect to be able to find patterns in the data.  The concerns I have are:

If the datasets are sufficient to discern patterns with high enough model performance to be useful
Network data can be like looking at static on a TV screen--if you stare at it long enough, you start to see things--so I want to avoid the classification version of hallucinations
If my padwan-level data science skills are up to the task :)
Why this question is important

Data networks are central to every day life for both people and businesses so well operating networks are to everyone's benefit.  Most network operations tools are reactive in nature today (quickly identifying root cause analysis and possible resolutions).  Being able to proactively identify issues before they become noticeable and service impacting would be a huge benefit both to the companies that operate these networks and the employees and customers that use them.
