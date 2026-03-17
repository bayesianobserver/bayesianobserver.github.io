---
layout: post
title: "Document as a Database"
date: 2012-09-30
original_url: "https://thebayesianobserver.wordpress.com/2012/09/30/document-as-a-database/"
categories: ["machine-learning"]
---
The problem with conventional text documents is that you cannot easily query them. Suppose I have a 20 page piece of text explaining various things, perhaps with mathematical equations, and plots, etc. In order to figure out something, I need to patiently read through the document till I have my answer. When time is short, and usually time is short, I will skip some parts in a hurry to get to what I need. The skipped parts might contain intermediate facts or definitions, making it impossible for me to understand what I am looking for even when I do find it.

This situation is because information is being presented in the document in an order decided by the author. Perhaps this is the best order. But for a specific query (e.g. what is the main result of this paper? ), it would be nice to have a way to do better than having to patiently read the whole document. The best we have right now is Ctrl+F on words and phrases, which just doesn’t cut it for queries of reasonable complexity (e.g. ‘Why did the GDP of Germany double so quickly?’ while reading an article on the history of the German economy).

The computer doesn’t understand the document 😦

It would be pretty useful to somehow model documents as databases that can support complex queries. Especially when the documents are large, like books. Perhaps I am asking for the holy grail of NLP? Surely, if IBM can build a Jeopardy-winning Watson, it should be possible to build a question-answering service for individual documents? Outside information is permitted.
