## Brief EDA Process

### 1. Data Preprocessing
The first step in the EDA process was data preprocessing. This involved cleaning and organizing the raw data to ensure it was in a format suitable for analysis. Common preprocessing tasks included handling missing values, encoding categorical variables, and scaling numerical features.

### 2. Handling Web Scraping Parsing Errors
To enhance the quality of the data, it is identified and addressed parsing errors that may have occurred during web scraping. This step specifically focused on cleaning categorical columns where web scraping errors were present, ensuring the accuracy and reliability of the data.

### 3. Exploring Correlations
Correlation analysis was performed to understand the relationships between different variables in the dataset. By identifying correlations, we gained insights into potential patterns and dependencies, which can be crucial for understanding the underlying structure of the data.

### 4. Analyzing Word Frequencies
An important aspect of the analysis was examining word frequencies within relevant text data. This involved tokenizing and counting the occurrences of words to uncover common themes or patterns. Understanding word frequencies can provide valuable information, especially when dealing with text-heavy datasets.

# Text Embeddings for Duplicate Detection

## Why BERT?

### 1. Contextual Embeddings
BERT is a state-of-the-art transformer-based model that generates contextual embeddings. Unlike traditional word embeddings such as FastText, GloVe, or Word2Vec, BERT considers the entire context of a word in a sentence. This contextual understanding is crucial for capturing the nuanced meanings of words in different contexts, making BERT highly effective for applications like sentence similarity.

### 2. Pre-training on Large Corpora
BERT is pre-trained on massive amounts of text data, enabling it to capture rich semantic information from diverse contexts. This pre-training allows BERT to learn intricate patterns and relationships within the language, making it proficient at understanding the semantics of sentences.

### 3. Robust Representation of Semantic Meaning
BERT provides a robust representation of semantic meaning by considering the bidirectional context of words. This is particularly advantageous for tasks where understanding the meaning of an entire sentence is essential, as is the case with identifying duplicate or similar sentences.

### 4. Comparison with FastText, GloVe, and Word2Vec

While FastText, GloVe, and Word2Vec are effective for many natural language processing tasks, they have certain limitations that influenced my decision:

Lack of Contextual Information: FastText, GloVe, and Word2Vec generate static embeddings and do not consider the contextual information of words. This limitation can affect their performance in tasks that require an understanding of word meaning in different contexts.
Inability to Capture Long-range Dependencies: BERT's attention mechanism allows it to capture long-range dependencies between words in a sentence, providing a more comprehensive understanding compared to traditional word embeddings. This is especially important since the descriptions arguably long.

## How parameters are decided?

### Threshold

In cases where precise matches are crucial, a lower threshold may be warranted. However, my observation of the data led me to believe that a threshold of 0.2 strikes an appropriate balance for the particular use case. The decision-making process involved extensive empirical testing. I experimented with different threshold values, evaluating their impact on the identification of similar items. Through this iterative process, I gauged the performance of the system and converged on a threshold that maximizes the utility of the similarity search.

### Milvus Parameters

The choice of "L2" metric and the nprobe parameter in search_params reflects a conscious effort to balance recall and search efficiency. A value of 16 suggests a middle ground, aiming for reasonably accurate results without sacrificing too much on search speed.
The use of "IVF_FLAT" in index_params indicates a preference for the Inverted File structure with Flat indexing. This is a well-suited strategy for large-scale vector databases, providing an efficient trade-off between storage requirements and search performance.

## Other Use Cases
  1) Discovering similar job opportunities.
  2) Recommending other suitable positions based on the applied job description.
  3) Highlighting distinctive job descriptions/requirements for job posters compared to other similar positions

## Milvus Database Setup and Job Posting Data Deduplication

### Introduction

This repository outlines the process of setting up a Milvus database on a notebook, utilizing Docker for managing the Milvus database. The project focuses on storing and managing job posting data, implementing a deduplication mechanism to avoid storing duplicate entries. The goal is to demonstrate the efficiency of Milvus, particularly in handling large datasets and employing approximate nearest neighbors (ANN) architecture to enhance search performance.


### Dockerization

Docker is used to containerize the Milvus database, making it easily deployable and reproducible. The provided Dockerfile ensures a consistent environment for running Milvus.

### Connectivity Challanges

The initial strategy involved developing a FastAPI application that receives a description, extracts its embeddings, checks the database for duplicates, and adds the description to the database if it's not a duplicate. However, we encountered a setback when attempting to establish a connection to Mulvis from another Docker container, ultimately leading to an unsuccessful implementation.

## Setup Milvus Docker

### Start Milvus
```sudo docker-compose up -d```


