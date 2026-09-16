---
title: "Yonder RecSys"
description: "A vector-search recommendation engine, built as a take-home assignment for an interview process."
tags: ["Python", "RAG", "Recommender Systems"]
project_tags: ["Python", "RAG", "Recommender Systems"]
---

`Python`

[View on GitHub](https://github.com/ArunGautham-Soundarrajan/yonder-recsys)

`yonder-recsys` is a recommendation engine that suggests personalized experiences to users based on their transaction history and past activity, filtered by location. It was built as a take-home assignment for an interview process, under a real-world brief and time constraint rather than as an open-ended personal project.

It's built with FastAPI, uses Milvus for vector search over OpenAI embeddings, and combines that retrieval step with an LLM to rank and contextualize the final recommendations — the same retrieval-plus-ranking pattern behind most of my recent interest in search systems.
