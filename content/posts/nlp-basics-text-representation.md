+++
date = '2021-09-24'
draft = false
title = 'NLP Basics: Text Representation and Similarity'
tags = ['NLP']
summary = 'A quick grasp on cosine similarity by understanding vectors and similarity metrics.'
+++

A quick grasp on cosine similarity by understanding vectors and similarity metrics.

## The Problem

Let's imagine you work for NASA and you have received a new message from an unknown species from space. You were asked to identify if it's a threatening or a friendly message. You don't know their language and all you have is two messages previously received from them. Luckily they both were identified as threatening or friendly. What if you could compare your new message with the previous ones to identify how similar they are?

- **Message 1:** We love earth (Friendly)
- **Message 2:** We hate human's (Threatening)
- **New message:** We love animals in earth (?)

Okay, now that we have the messages, how do we compare them? We all know that computers know only numbers. So we need a way to represent text numerically. Let's look at common ways of representing text in numbers.

## Representation of Text

### Notations

- **Collection:** A set of text documents is called a collection. In our case, the three messages represent a text collection.
- **Vocabulary:** A set of all the unique words in the collection forms the vocabulary.

### One-Hot Encoding

One-Hot Encoding represents text in a vector form for each document. As the name suggests, if a word is present in the document, it is represented as 1 and 0 if not. The dimension of this vector is the size of the vocabulary and it's the same for all the documents in the collection.

### Bag of Words

The issue with the One-Hot representation was it doesn't stress the importance of a word in a document. Every word is treated equally if they are present. But in reality, if a word appears more than the other words, it means something. That's why we bring in the term frequency, which represents the frequency of a term in a document. This representation is called the bag of words representation.

**For example:**

```
'We love human's, human's love us'
```

But does term frequency work? Words that appeared more don't mean that they are important. For example, an article about cars probably contains multiple occurrences of the word "car", but a word that does occur only in that document can be used to differentiate it from others. That's where we bring in **inverse document frequency**. This is found by dividing the total number of documents in the collection by the number of documents containing that term. This IDF (Inverse Document Frequency) is combined with Term Frequency to give **TF-IDF**, which is widely used.

#### Understanding TF-IDF

This is one of the many available variants of this formula. The log is used to dampen the effect of linear scaling, so higher values won't scale up too quickly. For example:

- log(10) = 3.32
- log(20) = 4.32

This reduces the effect of large values.

#### Importance of Log in TF-IDF

**Example:**

- N = 100
- df = 5
- idf = 100/5 = 20
- tf = 10
- tf-idf (without log) = 10 × 20 = 200

**With log:**

- tf-idf = (1 + log(10)) × log(20)
- tf-idf = 3.32 × 4.32 = 14.34

Notice the significant difference! We can do this calculation for every term to get a vector representation.

## Text Similarity Metrics

We now have the vector representation of words. What can we do with vectors? Generally, similar things lie close to each other. If we plot these vectors in a high-dimensional space, we can measure how close they are to find similarities. For this, we use **cosine similarity**.

_Cosine similarity by Ramni Harbir Singh, et al._

### Cosine Similarity

Cosine Similarity is the measure of the angle between two vectors in a multidimensional space. The angle between the same vector is 0, so the lesser the angle between two vectors, the more similar they are.

From the trigonometric relationship, we can derive the final formula. Where `a` and `b` can be any vectors (in our case, messages):

```
cosine_similarity(a, b) = (a · b) / (||a|| × ||b||)
```

### Solving Our Problem

The Bag of Words (Term Frequency) vector representation of three messages:

```
M1 = (1, 1, 1, 0, 0, 0, 0)
M2 = (1, 0, 0, 1, 1, 0, 0)
M3 = (1, 1, 1, 0, 0, 1, 1)
```

**Important:** To compare vectors, they all should be in the same space—same dimensionality and order of words.

After calculation of cosine similarity, cosine similarity ranges between 0 to 1, where:

- **1** = most similar
- **0** = no similarity

This is because the angle for the same vector is 0 and cos(0) = 1.

From our calculation, Message 1 and Message 3 are similar, so it is a **friendly message**, which seems correct!

**Voilà!** You have found the similarity between the two texts without the need of understanding them. That's math for you.

## Disadvantages

- **Sparsity:** Vector representation suffers from sparsity as most of the vectors are 0. A collection with 1000 unique words requires 1000 dimensions, and ML models suffer from the curse of dimensionality.
- **Order:** This representation doesn't account for the order of the words, which is very important. For example, "Joe loves Jane" and "Jane loves Joe" have different meanings, and this information is not preserved.

## Further Reading

- Word2Vec
- Contextual Word Embeddings (BERT, ELMo)
