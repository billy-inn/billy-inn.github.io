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

**Week 1 (5.8-5.14)** 

- First meeting with my mentor
- Create the public page for the project
- Create the google doc for the project

**Week 2 (5.15-5.21)**

- Get the [existing mappings](http://mappings.dbpedia.org/server/mappings/en/pages/rdf/all)
- Get the information about all templates: [https://github.com/dbpedia/extraction-framework/tree/master/server/src/main/statistics](https://github.com/dbpedia/extraction-framework/tree/master/server/src/main/statistics)
- Parse and clean the data

**Week 3 (5.22-5.28)**

- Figure out the information we have:
    - 1) Existing mappings, we have manual information that a template in lang $X$ is mapped to class $Y$
	- 2) Inter-language links between templates, e.g. template $X_1$ in lang $X$ is mapped to class $Y$ and there is a link from this template to templates in other languages. This gives a high probability that the equivalent templates in other languages should be mapped to the same class $Y$.
	- 3) Links between articles in different languages and templates each article uses, this way, when (2) is not always true we can find which templates are used for the same concepts. 
	- 4) Most wikidata articles have a type assigned, using this information we have a variation of  metric (3) but with manual types assigned.
- Process the information (1) - (3) described above and obtain some prelimenary results.

**Week 4 (5.29-6.4)**

- Propose a baseline approach: Given a template classified as an infobox, the approach is instance-based and exploits the already mapped articles and their cross-language links to the articles that contain the template to be mapped. This approach is summaried in the below figure.

![Alt text](/images/GSoC.png)

- Experiments:
    - Based on existing mappings in English, to create mappings for Chinese.
	- Evaluations: try this approach on some other languages which have some existing mappings. (In progress)
