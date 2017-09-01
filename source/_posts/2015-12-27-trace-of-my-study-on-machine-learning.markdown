---
layout: post
title: "Trace of My Study on Machine Learning"
date: 2015-12-27 17:38:14 -0700
comments: true
categories: machine_learning
---

This blog will record the timeline, resources, projects along the way of my study on machine learning since 2015. And I will keep updating this blog.

### Mathematics

- Basics: better to review before real study of ML
    - Calculus
	- Linear Algebra
		- [Introduction to Linear Algebra](http://math.mit.edu/~gs/linearalgebra/): a nice textbook in linear algebra (**First Pass** in *Dec, 2015*).
		- [MIT 18.06](https://www.youtube.com/watch?v=ZK3O402wf1c&list=PLE7DDD91010BC51F8): Linear algebra (**Completed** in *Dec, 2015*).
	- Probability Theory
- Reference
	- [Handbook of Mathematics](http://www.springer.com/us/book/9783662462201): an amazing reference book of mathematics.
- Statistics
	- [All of Statistics](http://www.stat.cmu.edu/~larry/all-of-statistics/): A textbook appealing to MLers (**First Pass** in *Aug, 2017*).
	- [Statistical Inference](http://www.amazon.com/Statistical-Inference-George-Casella/dp/0534243126): Classic textbook.
	- [CMU 10-705](http://www.stat.cmu.edu/~larry/=stat705/): Intermediate Statistics (**Completed** in *Aug, 2017*).
	- Post Series: Doubt Clarification for Statistics (In *Chinese*)
		- 1\. [What is p-value?](/blog/2017/07/28/p-value/)
		- 2\. [What's the usage of probability inequalities](/blog/2017/08/09/probability-inequalities/)
		- 3\. [Law of Large Numbers and Central Limit Theorem](/blog/2017/08/17/lln-and-clt/)
- Optimization
	- [Convex Optimization](http://web.stanford.edu/~boyd/cvxbook/): Classic textbook.
	- [Stanford EE364a](http://stanford.edu/class/ee364a/index.html): Convex Optimization.
- Advanced Topics on Linear Algebra
	- [The Matrix Cookbook](http://www2.imm.dtu.dk/pubdb/views/edoc_download.php/3274/pdf/imm3274.pdf): Ongoing
	- [Matrix Analysis](https://www.amazon.ca/Matrix-Analysis-Roger-Horn/dp/0521548233): Ongoing

<!--more-->

### Statistical Machine Learning

- [Coursera: Machine Learning](https://www.coursera.org/learn/machine-learning): Introduction to machine learning. ([Certificate](/certificates/ml.pdf))
- [StanfordOnline: Statistical Learning](https://lagunita.stanford.edu/courses/HumanitiesandScience/StatLearning/Winter2015/info): Introduction to statistical learning and **R**. ([Certificate](/certificates/sl.pdf)) 
- [UAlberta CMPUT 466/551](https://www.ualberta.ca/computing-science/undergraduate-studies/course-directory/courses/machine-learning): Machine Learning. I'm one of TAs in this course.
	- Post Series: ML with R
		- 1\. [Linear Regression](/blog/2016/08/31/ml-with-r-1-linear-regression/)
		- 2\. [Regularized Linear Regression](/blog/2016/09/14/ml-with-r-2-regularized-linear-regression/)
		- 3\. [Logistic Regression](/blog/2016/09/20/ml-with-r-3-logistic-regression/)
- [The Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/): Ongoing
    - [Manual](http://waxworksmath.com/Authors/G_M/Hastie/hastie.html): Figure out the mathematical details.
	- [R package "ElemStatLearn"](https://cran.r-project.org/web/packages/ElemStatLearn/index.html): Contain data sets, functions and examples from the book.
	- [My code](https://github.com/billy-inn/ElemStatLearn): Exercises and experiment reimplementations in **R**.

### Probabilistic Graphical Models:

- [UAlberta CMPUT 659](https://uofa.ualberta.ca/computing-science/graduate-studies/course-directory/courses/probabilistic-graphical-models): Probabilistic Graphical Models. Graduate course in University of Alberta based on Coursera course instructed by [Koller](http://ai.stanford.edu/users/koller/) ([Report: A Topic Model of Genetic Mutations in Cancer](/papers/cmput659.pdf), **Completed** in *Apr, 2016*).
- [CMU 10-708](http://www.cs.cmu.edu/~epxing/Class/10708-15/lecture.html): Probabilistic Graphical Models.
- [Probabilistic Graphical Models: Principles and Techniques](http://pgm.stanford.edu/): Classic textbook for probabilistic graphical models. I've read a few chapters of it and gave up. This book is somewhat too mathematical and I will not recommend this book for beginners in PGM.
- [Pomegranate](https://github.com/jmschrei/pomegranate): A Python package for PGM. Nice tutorials for beginners in PGM!

### Deep Learning

- [Neural Network and Deep Learning](http://neuralnetworksanddeeplearning.com/index.html): Nice online tutorial for beginners in deep learning (**Completed** in *Sep, 2016*).
- [Coursera: Neural Networks for Machine Learning](https://www.coursera.org/learn/neural-networks): Excellent course for beginners in neural networks. ([Certificate](/certificates/NN4ML.pdf))
- [Stanford CS224d](http://cs224d.stanford.edu/): Deep Learning for Natural Language Processing (**Completed** in *Apr, 2017*).
- [Stanford CS231n](http://vision.stanford.edu/teaching/cs231n/index.html): Convolutional Neural Networks for Visual Recognition.
- [Deep Learning Book](http://www.deeplearningbook.org/): Ongoing.
- [TensorFlow](https://www.tensorflow.org/): Large amount of high-quality tutorials and well-coded recent advances in DL. Most applicable scenario: research.
- [Mxnet](https://github.com/dmlc/mxnet): High performance. Most applicable scenario: industry.
- [Keras](https://keras.io/): High-level, easy to use. Most applicable scenario: competitions like Kaggle.

### Large Scale Machine Learning

- [edX: Introduction to Big Data with Apache Spark](https://courses.edx.org/courses/BerkeleyX/CS100.1x/1T2015/info): Introduction to Spark in **Python**. ([Certificate](/certificates/spark.pdf))
- [edX: Scalable Machine Learning](https://courses.edx.org/courses/BerkeleyX/CS190.1x/1T2015/info): Explore deeper usage of Spark on large scale machine learning. ([Certificate](/certificates/scalableML.pdf))
- [Coursera: Functional Programming Principles in Scala](https://www.coursera.org/learn/progfun1/): Introduction to **Scala**. ([Certificate](/certificates/fpp.pdf))
- [Coursera: Functional Program Design in Scala](https://www.coursera.org/learn/progfun2): Further study on **Scala**. ([Certificate](/certificates/fpd.pdf))
- [Coursera: Parallel Programming](https://www.coursera.org/learn/parprog1): Parallel computing in **Scala**. ([Certificate](/certificates/pp.pdf))
- [Coursera: Big Data Analysis with Scala and Spark](https://www.coursera.org/learn/scala-spark-big-data): Intro to **Spark** with **Scala**. ([Certificate](/certificates/ScalaAndSpark.pdf))
- [Coursera: Big Data Analysis with Scala and Spark](https://www.coursera.org/learn/scala-spark-big-data): Intro to **Spark** with **Scala**. ([Certificate](/certificates/ScalaAndSpark.pdf))
- [Coursera: Functional Programming in Scala Capstone](https://www.coursera.org/learn/scala-capstone): Capstone project for **Scala**. ([Certificate](/certificates/ScalaCapstone.pdf))

### Reinforcement Learning

- [UAlberta CMPUT 609](https://www.ualberta.ca/computing-science/graduate-studies/course-directory/courses/reinforcement-learning-in-ai): Reinforcement Learning. Graduate course in UofA instructed by [Sutton](https://webdocs.cs.ualberta.ca/~sutton/). ([Report: Investigation on Deep Reinforcement Learning Methods for Classical Control Problems](/papers/cmput609.pdf), **Completed** in *Dec, 2016*). 
- [Introduction to Reinforcement Learning](https://webdocs.cs.ualberta.ca/~sutton/book/the-book.html): Classic textbook, recommended for beginners in RL (**First Pass** in *Dec, 2016*).
- Post Series: Notes on Reinforcement Learning
	- 1\. [Finite Markov Decision Processes](/blog/2016/10/05/notes-on-reinforcement-learning-1-finite-markov-decision-processes/)
	- 2\. [Dynamic Programming](/blog/2016/10/06/notes-on-reinforcement-learning-2-dynamic-programming/)
	- 3\. [Monte Carlo Methods](/blog/2016/10/14/notes-on-reinforcement-learning-3-monte-carlo-methods/)
	- 4\. [Temporal-Difference Learning](/blog/2016/10/16/notes-on-reinforcement-learning-4-temporal-difference-learning/)

### Data Mining

- [Coursera: Mining of Massive Datasets](https://www.coursera.org/course/mmds): Introduction to a lot data mining techniques. ([Certificate](/certificates/mmds.pdf))

### ML Competitions

- [Kaggle: Home Depot Product Search Relevance](https://www.kaggle.com/c/home-depot-product-search-relevance): Top 10%. ([Report](/papers/cmput690.pdf))
