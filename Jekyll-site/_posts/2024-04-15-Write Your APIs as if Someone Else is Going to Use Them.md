---
layout: post
title: "Write Your APIs as if Someone Else is Going to Use Them"
description: "Principles I personally follow while designing and writing an API"
date: 2025-04-15
tags: [software engineering]
---

It's easy to fall into the trap of designing APIs for yourself or your immediate team — especially when deadlines are looming or you're the only one consuming them initially. But one of the most important lessons I've learned through experience — particularly after working on numerous third-party integrations — is this:

**Design your APIs like someone else — someone you've never met — is going to use them.**

Because chances are, they will.

Whether it's a new developer on your team, an external partner, or even your future self six months down the line, your API will eventually serve someone who wasn't part of the original design conversation. And if you've ever had to reverse-engineer a poorly documented or inconsistent third-party API, you know just how painful that can be.

## Good APIs Feel Like Products

Think about the APIs you've enjoyed working with. They're probably well-documented, intuitive, consistent, and surprisingly easy to integrate. The Slack API is a great example — it's clear, predictable, and built with developers in mind. You don't need to read an entire manual before making your first request. Everything just works the way you expect it to.

That's not an accident. It's a product mindset applied to internal tooling.

## My Approach to API Design

These are not universal rules, but principles I personally try to follow when designing APIs — ones that have helped me create interfaces that are easy to use and maintain.

### 1. Clarity Over Cleverness

Avoid over-engineering. Use descriptive endpoint names and payload structures. Stick to standard HTTP methods (GET, POST, PUT, DELETE) and make sure their behavior aligns with expectations.

✅ `GET /users/123`  
❌ `POST /doActionOnUser`

### 2. Consistency Is Key

Maintain consistent naming conventions, response formats, and error structures across your API. If one endpoint returns an object with a `user_id`, don't call it `id_user` elsewhere.

### 3. Design for Errors

Great APIs don't just succeed gracefully—they fail gracefully too. Use standard status codes, return meaningful error messages, and provide actionable information in your responses.

```json
{
  "error": "Invalid request",
  "details": "The 'email' field is required"
}
```

### 4. Single Responsibility: Do One Thing Well

Each endpoint should have a single, clear responsibility. Don't combine actions like "create and assign and notify" in one API call. That makes behavior harder to predict and harder to reuse. Simpler, atomic endpoints are easier to test, understand, and maintain.

✅ POST /users — Creates a user  
✅ POST /assignments — Assigns a task  
✅ POST /notifications — Sends a notification  
❌ POST /do-everything

### 5. Write Friendly Documentation

An API without documentation is a puzzle. Provide clear, concise guides, request/response examples, and use cases. Great docs reduce support requests and increase developer adoption.

### 6. Think Use Case First — But Don't Overfit to Clients

While it's helpful to consider real-world workflows, your API shouldn't be overly shaped by a single client's specific use case. That leads to rigid design and tightly coupled behavior. Instead, aim to build general-purpose, composable APIs that work across a variety of scenarios.

If the client needs a shortcut or bundling of multiple operations, they can do that on their side using your clean, granular APIs.


## The Developer Experience is the Product

When you treat your API as a product, you think about the developer experience. This includes everything from onboarding and authentication, to naming, documentation, and how errors are handled.

A well-designed API can become a growth engine. It can enable integrations, open up your platform to partners, and make internal teams more productive. A poorly designed one? It becomes a liability.

## Final Thoughts

Building APIs isn't just a backend task. It's an act of communication. And just like good code tells a story that's easy to read, a good API should be intuitive, consistent, and user-focused.

So, next time you design an endpoint, ask yourself:
Would this make sense to someone who knows nothing about my codebase?
If the answer is yes, you're on the right track.

These are the standards I hold myself to — not hard rules, but guiding principles that have served me well. If they help you too, even better.
