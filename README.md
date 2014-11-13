Predicting Wikipedia Election Outcomes
============

Wikipedia administrators are Wikipedia editors granted privileges like blocking and unblocking user accounts, viewing and restoring deleted pages, 
and restricting editing of a particular page [1]. Of the 22 million registered Wikipedia users, about only 1,400 are administrators and requests
for adminship have a 4 in 10 chance of acceptance [2]. To become a Wikipedia admin, one must either nominate themselves or be nominated. In either 
case, the Wikipedia community will be the judge of a prospective admin, rating them positively, negatively, or neutrally.  

Given a network of Wikipedia users and data on their participation in Wikipedia, our project will try to predict whether a user will be elected 
as a Wikipedia administrator. 

Dataset
======

Wikipedia Adminship Election Data [3] - Data from the actual election, including user votes for candidates, the time in which the vote was cast, and the final election results (helps test whether our models are successful).

Requests for Adminship [4] - Adminship requests submitted either by the candidate in question, or by other community members. May be helpful for identifying communities.

Wikipedia Edit History [5] - Edit history that may be helpful for identifying communities or determining the reputation of admin nominees/nominators. This dataset has a combined size of ~3 TB (18GB compressed), so it is not exactly wieldy and will probably be sparsely used, if at all.

Wikipedia Talk Network Data [6] - Data which contains an edge (a, b) if a has once edited the talk page of b. Can be used to model communication between users and aid in detection of user communities.

Features
=====
There are a number of potential features we could incorporate into our model, using the datasets mentioned above. There is some data available from the elections dataset itself, including nominating user, timestamp, and voter identities. However, we can also draw a significant amount of features from auxiliary sources, such as the edit history graph (to find the identity of the user’s most-edited pages) and the talk page network (to determine users with whom they communicate most). Applying techniques for graph structural analysis to these datasets may yield additional features, such as talk network degree, PageRank value, or community identity.

Models
=====
The plethora of data allows us to model the network of Wikipedia users in several different ways, each of which we may draw inferences from to guide the outcome of our hypothesis. Adminship election data may be modeled as a signed or weighted network, requests for adminship modeled as a directed network with self-loops. Talk data is given as a directed graph. We may also create a single weighted graph where the weights are drawn from a function which take into account multiple datasets.

Community-detection algorithms (i.e. NCP or Spin-Glass) may be used to better understand the structure of the clusters and communities within the network of Wikipedia users. Users have varying levels of influence and reputation, which we may attempt to quantify using algorithms such as PageRank. We may also use a role-finding algorithm 

To predict the actual elections, we will attempt to reduce the election to a binary classification problem, based on the network metrics that we have mentioned above. We may first start off with a simpler model, such as Naive Bayes or Newton’s method.

Notes 
=====
The Wikipedia datasets are all very large, and will require some big data computing power for processing. We hope to use Stanford SNAP (if on a monolithic machine), or GraphLab, Apache Hadoop, or Apache Spark on a service like Amazon EC2 for this purpose.
Our work on this problem may have potential use for predicting reputation on other wikis or wiki-structured sites. It may also have applicability in other content-based social networks.

References
======
[1] “Wikipedia: Administrators.” Wikipedia: The Free Encyclopedia. Wikimedia Foundation, Inc., 5  Oct. 2014 Web. 16 Oct. 2014

[2] “Wikipedia: Requests for adminship/Nominate.” Wikipedia: The Free Encyclopedia. Wikimedia Foundation, Inc., 24  Sept. 2014 Web. 16 Oct. 2014

[3] https://snap.stanford.edu/data/wiki-RfA.html

[4] http://snap.stanford.edu/data/wiki-RfA.html

[5] http://snap.stanford.edu/data/wiki-meta.html

[6] http://snap.stanford.edu/data/wiki-Talk.html 
