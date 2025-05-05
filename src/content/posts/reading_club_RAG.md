---
title: reading_club_RAG
published: 2025-05-02
description: ' This is only about the paper of in context RAG'
image: ''
tags: ['RAG', 'in context RAG', 'LLM']
category: 'RAG'
draft: false 
lang: 'en'
---

Hi guys, this reading club is suppoed to be hold on 6th May. 

The go thorugh would be too random. Hope you could read by yourself. Or maybe you could find a better blog to read. ^^

It is about the paper of in context RAG [arxiv](https://arxiv.org/abs/2302.00083). Cool, let's start.

I have read the paper and I would not cover chapter by chapter but cover the topic I did not know before and then move forward to what I am interested in.

## What is RAG? Why we need it? What we should suppose it be able to do?

RAG is a complementary technique to LLM. It is a technique to improve the performance of LLM. It is well-known as a bunch of documents or storage of bunch of knowledge. Either LLMs have access to the knowledge or not, RAG is able to enriched the LLM's attention to this part. but RAG is not a static storage. It is a dynamic storage. It involves a whole process of retrieval, ranking, and reranking.

For an example, LLM might be good at giving the previous history but have no access to news. RAG is able to give the news to LLM. Another example is that despite LLM already learned the knowledge but some time it might mislead to wrong information. RAG could be able to fix that.

### I heard some blog said that RAG is not as important as former since LLM is able to provide the answer by itself. 

I do not know if I understand is correct or not. It is more like an extra work technique during the infering process. Even with base model performance evolve, RAG should be valuable for some case: not common knowledge, not common question, not common context.

## What is in context RAG? What is the difference between in context RAG and RAG?

They said a lot of bad word or difference between in context RAG and RAG. I do not know if it is true or not since when I just summarize and repeat to LLM, they would say that is not so true.

The main difference is that RAG commonly provide a retrieval result as some embedding or vector or some other way. In context RAG is simpler. It just provide the query response to LLM. no extra training. Easy to use.

Beside that, very important thing is that it did not stop at the new structure of RAG, but also systematical analysis of the performance of RAG with a frequent retrieval. (result said more frequent retrieval is better)

## What is the performance of in context RAG in this paper?

Improve the performance of Multiple or said all LLM with lower perplexity. 

result 2: BM25 which is a variant of TF-IDF is better than all the encoder representation including BERT or other BERT-like model.

They propose a very interesting design of the study. One is changable Retrieval stride that they can change the retrieval to change the frequency of retrieval. retrieval query length: since different LLM might have different context window, they can change the query length to see the performance.

Result 3: they use a stride 4 instead of a common 64. so it is much more frequent retrieval. Result is that the frequency of retrieval is like a effience and effectiveness delimma: you cannot hold both.

retrieval query length does not show large impact as the frequency did. For their task and model the bes one is query with 32 length. From my perspective, the number of the length should vary with different task at least and for model, might vary as well.

Increase the range of the candidate could improve the performance a lot. 

## Good innovation: LMs as a zero shot reranker

They use a same model to do the reranking. It is more like a compensation for the BM25 since BM25 is not abled with the content understanding.
