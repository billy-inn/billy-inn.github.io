---
layout: post
title: "GSoC 2016: Inferring infobox template class mappings from Wikipedia and WikiData"
date: 2016-04-26 15:51:27 -0600
comments: true
categories: Project 
---

*This page is the public project page and will be updated every week.*

### Project Description

There are many infoboxes on wikipedia. Here is a example about football box:

![Alt text](/images/GSoC1.png)

As seen, every infobox has some properties. Actually, every infobox follows a certain template. In my project, the goal is to find mappings between the classes (eg. ```dbo:Person```, ```dbo:City```) in the DBpedia ontology and infobox templates on pages of Wikipedia resources using techniques of machine learning.

There are lots of infobox mappings available for a few languages, but not as many for other languages. In order to infer mappings for all the languages, cross-lingual knowledge validation should also be considered. 

The main output of the project will be a list of new high-quality infobox-class mappings.

<!--more-->

### Weekly Progess

**Week 1 (5.9-5.15)** 

- First meeting with my mentor
- Create the public page for the project
- Create the google doc for the project

**Week 2 (5.16-5.22)**

- Get the [existing mappings](http://mappings.dbpedia.org/server/mappings/en/pages/rdf/all)
- Get the information about all templates: [https://github.com/dbpedia/extraction-framework/tree/master/server/src/main/statistics](https://github.com/dbpedia/extraction-framework/tree/master/server/src/main/statistics)
- Parse and clean the data

**Week 3 (5.23-5.29)**
