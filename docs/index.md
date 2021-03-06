```eval_rst
.. toctree::
   :hidden:
   :maxdepth: 2
   
   self
   quickstart
   installation
   configuration
   yarn-hdfs
   faq
   latent-dirichlet-allocation
   med-lda
   dnn-general
   dnn-speech
   matrix-fact
   nonneg-matrix-fact
   sparse-coding
   lasso-and-lr
   distance-metric-learning
   k-means
   random-forest
   support-vector-machine
   multiclass-logistic-regression
```

# Overview

Petuum is a distributed machine learning framework. It takes care of the difficult system "plumbing work", allowing you to focus on the ML. Petuum runs efficiently at scale on research clusters and cloud compute like Amazon EC2 and Google GCE.

The Petuum project is organized into 4 open-source (BSD 3-clause license) Github repositories:
* [Bösen (C++ bounded-async key-value store)](https://github.com/petuum/bosen)
* [Strads (C++ model-parallel scheduler)](https://github.com/petuum/strads)
* [JBösen (Java bounded-async key-value store)](https://github.com/petuum/jbosen)
* [Poseidon (Deep Learning framework)](https://github.com/petuum/poseidon)

To install Bösen and Strads, please continue reading this manual. If you have a Java environment and want to use JBösen, please start [here](https://github.com/petuum/jbosen/wiki). If you wish to use Poseidon for Deep Learning, please go [here](https://github.com/petuum/poseidon/wiki).

## Petuum Bösen/Strads v1.1 manual

1. [Quickstart](quickstart.md)
    1. [Detailed Installation Instructions](installation.md)
    1. [Configuration and Machine Files for Petuum Apps](configuration.md)
    1. [Running on Hadoop clusters with YARN/HDFS](yarn-hdfs.md)
    1. [Frequently Asked Questions](faq.md)
1. ML Applications
    1. Topic Models
        1. [Latent Dirichlet Allocation (topic modeling)](latent-dirichlet-allocation.md)
        1. [MedLDA (supervised topic modeling)](med-lda.md)
    1. Deep Learning
        1. [Poseidon: Distributed Deep Learning Framework on Petuum](https://github.com/petuum/poseidon/wiki)
        1. [General-purpose Deep Neural Network (DNN)](dnn-general.md)
            1. [DNN for Speech Recognition](dnn-speech.md)
    1. Matrix Factorization and Sparse Coding
        1. [Matrix Factorization (collaborative filtering)](matrix-fact.md)
        1. [Non-negative Matrix Factorization (NMF)](nonneg-matrix-fact.md)
        1. [Sparse Coding](sparse-coding.md)
    1. Regression
        1. [Lasso Regression](lasso-and-lr.md)
    1. Metric Learning
        1. [Distance Metric Learning](distance-metric-learning.md)
    1. Clustering
        1. [K-means Clustering](k-means.md)
    1. Classification
        1. [Random Forest](random-forest.md)
        1. [Logistic Regression](lasso-and-lr.md)
        1. [SVM](support-vector-machine.md) (Newly added in v1.1)
        1. [Multi-class Logistic Regression](multiclass-logistic-regression.md)
1. Programming API
    1. [Bösen Bounded-Async Key-Value Store](Bosen-Bounded-Async-Key-Value-Store)
    1. [Strads Model-Parallel Scheduler](STRADS-Model-Parallel-Scheduler) (Coming soon)

## Introduction to Petuum

Petuum is a distributed machine learning framework. It takes care of the difficult system "plumbing work", allowing you to focus on the ML. Petuum runs efficiently at scale on research clusters and cloud compute like Amazon EC2 and Google GCE.

Petuum provides essential distributed programming tools to tackle the challenges of ML at scale: **Big Data** (many data samples), and **Big Models** (very large parameter and intermediate variable spaces). To address these challenges, Petuum provides two key platforms:

* Bösen, a bounded-asynchronous key-value store for Data-Parallel ML algorithms
* Strads, a scheduler for Model-Parallel ML algorithms

Unlike general-purpose distributed programming platforms, Petuum is designed specifically for ML algorithms. This means that Petuum takes advantage of data correlation, staleness, and other statistical properties to maximize the performance for ML algorithms.

ML programs are built around update functions that are iterated repeatedly until convergence, as the following diagram illustrates:

![Data and Model Parallelism](http://petuum.org/images/data_model_parallelism.png)

The update function takes the data and model parameters as input, and outputs a change to the model parameters. **Data parallelism** divides the data among different workers, whereas **model parallelism** divides the parameters among different workers. Both styles of parallelism can be found in modern ML algorithms: for example, Sparse Coding via Stochastic Gradient Descent is a data-parallel algorithm, while Lasso regression via Coordinate Descent is a model-parallel algorithm. The Petuum Bösen and Strads systems are built to enable data-parallel and model-parallel styles, respectively.

## Key Petuum features

* Runs on compute clusters and cloud compute, supporting up to 100s of machines
* **Bösen**, a bounded-asynchronous distributed key-value store for data-parallel ML programming
  * Bösen uses the Stale Synchronous Parallel consistency model, which allows asynchronous-like performance that outperforms MapReduce and bulk synchronous execution, yet does not sacrifice ML algorithm correctness
* **Strads**, a dynamic scheduler for model-parallel ML programming
  * Strads performs fine-grained scheduling of ML update operations, prioritizing computation on the parts of the ML program that need it most, while avoiding unsafe parallel operations that could hurt performance
* Programming interfaces for C++ and Java
* YARN and HDFS support, allowing execution on Hadoop clusters
* **ML library with 10+ ready-to-run algorithms**
  * Newer algorithms such as discriminative topic models, deep learning, distance metric learning and sparse coding
  * Classic algorithms such as logistic regression, k-means, and random forest

## Support and Bug reports

For support, or to report a bug, please send email to petuum-user@googlegroups.com. Please provide your name and affiliation; we do not support anonymous inquiries.
