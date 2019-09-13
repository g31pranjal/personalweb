---
title : "Wikie : retrieval system"
enddate :      2016-11-12T16:00:00Z+0530
date : 2016-10-12T16:00:00Z+0530
desc : A web retrieval system which uses user feedbacks to improve search results
author : in-arena
keyword : information retrieval, ir, search, retrieval, wikipedia, crawler, pagerank, elo ratings
layout : projectTemplate
---

PageRank is an excellent method to calculate the relevance among the documents by exploring the intrinsic structure of the WWW, the hyperlinks between page. However, the classic retrieval system does not take into consideration any info regarding to the popularity of the page and favoritism among the users. This info forms the non-retrieval which cannot be determined inherently and hence, explicit methods has to be employed to it into account.

Our retrieval system concerns tapping of the User Feedback on a set of retrieved results, which can be used as a rich set of information for improving upon the quality of the search results, since it gives information about the user's interest and preferences...   


The project incorporates user click-through information into an existing ranking system to improve results based on the data received from previous instances when the pages on similar query is served to a user. This is done by maintaining a score for each page in the collection, by means of Elo rating, a classical rating system for rating players in Chess, Tennis etc. 

### # Elo Rating

Elo rating is the system of rating used for evaluating teams/individuals in sports. We have used a similar system to evaluate the pages of the search result based on the user behaviour over the pages fetched by a search query. If the user clicks a page, its rating is increased while the rating of others is decreased proportionally based on the position in which the result occurs. This means, if the last result is clicked, which is the least expected, then its ranking will be boosted to the maximum, however, if the top result is clicked, then there will only be a slight increase increase in the rating. Similarly, for the pages that are not clicked, ratings are decreased in the order of position in which the results appear. 

In a way, the user behaviour is fed back in the system to improve the ratings, which ultimately affects the final rank of the page in future searches of similar query. As the number of evaluations of a query increases, the elo rankings (calculated by ratings), reach a constant which signifies the ordering based on the popularity of the page, irrespective of the PageRank.

### # block diagram for the whole system :
<img style="width: 70%;margin:auto;display:block;" src="/assets/img/proj-ir-1.png" />

### # modules of the project include :
- **crawling and scraping** : implemented in python, uses multi-threading for running simultaneous connections to web. Uses BeautifulSoup for scraping text.
* **Indexing** : Implemented in C++ for running efficiency over the corpus of scraped text. Implements usual pre-processing techniques of Information Retrieval for generating tokens such as stopword removal, normalization, HTML decoding, Stemming.
* **PageRank** : Implemented in python. Calculates the PageRank score of pages in the collection by recursively iterating till the error in the PageRank matrix is reduced to the order of -6.
- **Elo Rating** : Implements Elo rating for each page. The ratings get updated each time the User clicks on the search results served to him. 
- **Rank Merging** : Merging the the ranks obtained from 3 sources viz. Similarity with the query, PageRank, Elo based on the calculated weights. Weights are calculated depending upon the confidence of the Elo Ratings, i.e. initially Elo Rating of all pages are the same, hence no significant contribution, but as the Elo Ratings get updated multiple number of times, it is given significant contribution in determining the final rankings. The weightage of other rankings (similarity and PageRank) is likewise adjusted.
- **GUI** : Implemented in Django 1.10.


### <i class="fa fa-github"></i>&nbsp;Github
<a href="https://github.com/g31pranjal/wikie" target="_blank">https://github.com/g31pranjal/wikie</a> 
(no longer maintained)


### # working stats :
- 106,000 Wikipedia pages crawled, 1.4 M links extracted (~1 M unique)
- Size of raw data : 13.1 GB, Size of clean data : 1.7 GB
- 26 M edges in 1.4 M links 
- 14.3 M edges in 100,000 crawled pages
- ~2 M unique words in index
- total size of postings : 456 MB
- total number of tokens in all documents : ~73 M

### # made with passion by an awesome team :)
- [Varun Vasudevan](https://www.linkedin.com/in/varun-vasudevan-54970bba/), [Akshit Bhatia](https://www.linkedin.com/in/akshit-bhatia-773504a9/), [Neel Kasat](https://www.linkedin.com/in/neel-kasat-47221110b/), and, me ! at BITS Pilani.
