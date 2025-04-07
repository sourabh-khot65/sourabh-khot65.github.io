---
layout: post
title: "Implementing RAG with Typesense and Pinecone"
date: 2024-04-07 12:00:00 +0530
---

At Tacitbase, we recently improved our search capabilities by implementing Retrieval-Augmented Generation (RAG) using Typesense and Pinecone. Here's how we did it and what we learned along the way.

## The Challenge

Our existing search system was good at finding exact matches but struggled with semantic search and understanding context. We needed a solution that could:

1. Understand the semantic meaning behind search queries
2. Provide relevant results even with partial information
3. Scale efficiently with our growing dataset

## The Solution

We chose to combine Typesense for fast full-text search with Pinecone for vector embeddings. The implementation involved:

```go
func (s *SearchService) SearchWithRAG(ctx context.Context, query string) (*SearchResult, error) {
    // Generate embeddings for the query
    embeddings := s.embedder.Embed(query)
    
    // Search in Pinecone for similar vectors
    vectors := s.pinecone.Search(ctx, embeddings)
    
    // Enhance results with Typesense
    results := s.typesense.Search(ctx, query, vectors)
    
    return results, nil
}
```

## Results

The new system improved search relevance by 45% and reduced false positives by 30%. More importantly, it now understands the context behind queries and provides more accurate results.

If you're interested in implementing something similar, feel free to reach out. I'm always happy to chat about search infrastructure and RAG implementations. 