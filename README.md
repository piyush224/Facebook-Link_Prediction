# Facebook-Link_Prediction

## 1. Problem statement:
This aim of this project is to predict a link between any two people given a directed graph of 1780722 People(nodes) and 7550015 edges between them.
## 2. Data Overview
Datab is taken from facebook's recruting challenge on kaggle https://www.kaggle.com/c/FacebookRecruiting data contains two columns source and destination eac edge in graph
Data columns (total 2 columns):
source_node int64
destination_node int64
## 3. Mapping the problem into supervised learning problem:
Training samples are made by using several features such as -

-'jaccard_followers', 'jaccard_followees', 'cosine_followers', -'cosine_followees', 'num_followers_s', 'num_followees_s', -'num_followees_d', 'inter_followers', 'inter_followees', 'adar_index', -'follows_back', 'same_comp', 'shortest_path', 'weight_in', 'weight_out', -'weight_f1', 'weight_f2', 'weight_f3', 'weight_f4', 'page_rank_s', -'page_rank_d', 'katz_s', 'katz_d', 'hubs_s', 'hubs_d', 'authorities_s' -'preferential_attachment_followers -'preferential_attachment_followees

## 4. Business objectives and constraints:
-Model should be interpretable such that nodes with highest probability are selected for recommendatiion. -No low-latency requirement.

## 5. Performance metric used:
- precision - recall

## 6. Feature Engineering:

### 6.1 Similarity measures
#### 6.1.1 Jaccard Distance
http://www.statisticshowto.com/jaccard-index/

```
 J = | X intersection Y| / | X union Y |
```

#### 6.1.2 Cosine distance
```
 Cosie Distance = | X intersection Y | / SQRT(|X|.|Y|)
```
### 6.2 Ranking Measures


https://networkx.github.io/documentation/networkx-1.10/reference/generated/networkx.algorithms.link_analysis.pagerank_alg.pagerank.html

PageRank computes a ranking of the nodes in the graph G based on the structure of the incoming links.

<img src='PageRanks-Example.jpg'/>

Mathematical PageRanks for a simple network, expressed as percentages. (Google uses a logarithmic scale.) Page C has a higher PageRank than Page E, even though there are fewer links to C; the one link to C comes from an important page and hence is of high value. If web surfers who start on a random page have an 85% likelihood of choosing a random link from the page they are currently visiting, and a 15% likelihood of jumping to a page chosen at random from the entire web, they will reach Page E 8.1% of the time. <b>(The 15% likelihood of jumping to an arbitrary page corresponds to a damping factor of 85%.) Without damping, all web surfers would eventually end up on Pages A, B, or C, and all other pages would have PageRank zero. In the presence of damping, Page A effectively links to all pages in the web, even though it has no outgoing links of its own.</b>

### 6.2.1 Page Ranking
```
https://en.wikipedia.org/wiki/PageRank
```
### 6.3 Other Graph Features

#### 6.3.1 Shortest path:
```
Getting Shortest path between twoo nodes, if nodes have direct path i.e directly connected then we are removing that edge and calculating path.
```
#### 6.3.2 Checking for same community

#### 6.3.3 Adamic/Adar Index:
```
Adamic/Adar measures is defined as inverted sum of degrees of common neighbours for given two vertices.
```
#### 6.3.4 Is persion was following back

#### 6.3.5 Katz Centrality:
https://en.wikipedia.org/wiki/Katz_centrality
```
https://www.geeksforgeeks.org/katz-centrality-centrality-measure/
 Katz centrality computes the centrality for a node 
    based on the centrality of its neighbors. It is a 
    generalization of the eigenvector centrality.
```

#### 6.3.6 Hits Score
https://en.wikipedia.org/wiki/HITS_algorithm
```
The HITS algorithm computes two numbers for a node. Authorities estimates the node value based on the incoming links.
Hubs estimates the node value based on outgoing links.
```
### 6.4 Adding a set of features
```
we will create these each of these features for both train and test data points
    jaccard_followers
    jaccard_followees
    cosine_followers
    cosine_followees
    num_followers_s
    num_followees_s
    num_followers_d
    num_followees_d
    inter_followers
    inter_followees
```
### 6.5 Adding new set of features
```
we will create these each of these features for both train and test data points
    Weight Features
        weight of incoming edges
        weight of outgoing edges
        weight of incoming edges + weight of outgoing edges
        weight of incoming edges * weight of outgoing edges
        2*weight of incoming edges + weight of outgoing edges
        weight of incoming edges + 2*weight of outgoing edges
    Page Ranking of source
    Page Ranking of dest
    katz of source
    katz of dest
    hubs of source
    hubs of dest
    authorities_s of source
    authorities_s of dest
```
## 7. Result
```
Fited RandomForestClassifier With
Train f1 score 0.9652533106548414
Test f1 score 0.9241678239279553
```
