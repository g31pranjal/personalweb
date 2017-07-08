---
title : "Analytic for Metastudio"
enddate :      2015-07-25T09:30:00Z+0530
date : 2015-05-20T09:30:00Z+0530
desc : Setting up Analytics and visualization tools for an indigenous MOOC platform
author : in-arena
keyword : nlp, natural language processing, spn graphs, ai, artificial intelligence
layout : projectTemplate
---

*I worked on this project during my internship at HBCSE, TIFR, Mumbai in summer of 2015.*

### # Background

Metastudio is an indigenous MOOC Platform, which is being developed at Homi Bhabha Centre for Science Education, TIFR, Mumbai under the guidance of [Dr. G. Nagarjuna](https://en.wikipedia.org/wiki/Nagarjuna_G.). The project is an instance of gStudio, a generic collaborative platform for knowledge and information sharing, inspired by openEdx project. 

At the core of the technologies used to model gStudio, is a module called Gnowsys, which is a system of Semantic computing to create Knowledge graphs. Adapting to the gStudio framework, Gnowsys describes a set of rules that defines the types of nodes that can exist in the framework and their valid relationships with other node. 

### # Analytics for Metastudio

Our work was to create a basic analysis and reporting tool for the platform that captures user activities on the website. The idea was two folded : 

1.  To create a live news feed that reports the recent and relevant user activities that is going on around a particular user. Since the structure of the platform allowed the formation of groups of users that can collaborate to a specific topic, group activities was an intuitive thing to come up with. 

2. Generate a basic analysis of the pattern in which user is using the platform, which includes reporting the number of User sessions, last activity, total activities, average session duration, resources uploaded etc. The goal of this was to encourage and reward users for doing valuable activity on the website.

### # The approach 

We started by analysing the existing platform so as to find a suitable place to tap the user activities. We found that there existed a module that was used to capture all activities on the platform for the purpose of bench-marking other backend modules. A little tweaks to this module helped us to capture the other required information that we could use to generate activity feeds for an individual users and collectively for a group. 

The Analytics module, hence, is a derived module that works by performing analysis on the bench-marking data, that was available to us from before. This tweak helped us to prevent laying on extra overload in processing requests, which was a remarkable achievement in this project. Analytics module is nothing but a helper module that analyses the user logs by cleaning, processing and organising the activity data in a separate 'Analytics' model. 'Analysing' is supposed to be done when a user 'clicks' to know the analytics for either itself or for a group, and is cumulative in nature to avoid repeated computations. The collective analytics for all users in the group is used to generate group analytics.

We even created an API-based approach to register other activities on the page that were not being captured at the backend. Such activities can be captured by giving a request at a specific URL using JavaScript from frontend along with the necessary details about the activity.

### # Aftermath

The project was the very initial building stone for a much bigger domain that Analytics can be. It was indeed a great pleasure and satisfaction to witness our project being merged to the main development branch. 

The following is a brief report for our complete projects that outlines the alterations and inclusions we did on the existing Metastudio project. 

####<a href="/assets/ps1-report.pdf" target="_blank"> <i class="fa fa-download"></i>&nbsp;Analytics for MetaStudio : the complete report</a>

### <i class="fa fa-github"></i>&nbsp;Github
<a href="https://github.com/g31pranjal/gstudio" target="_blank">https://github.com/g31pranjal/gstudio</a>

### # we did it :)

- Akshit Bhatia, Himanshu Singh Dhoni, Shubhi Rastogi and me at HBCSE, TIFR, Mumbai <3
- the list would be incomplete with the mentions of <a href="https://github.com/kedar2a" target="_blank">Kedar Aitawdekar
</a> and <a href="https://github.com/katkamrachana" target="_blank">Rachana Katkam </a>


