---
title: The Strategy of Scripting with the Lex Machina API
date: 2023-07-19T10:00:00-04:00
authors: [Dave Slusher]
draft: true
description: Writing scripts with the Lex Machina API have a recognizable design pattern
lead: Writing scripts with the Lex Machina API have a recognizable design pattern
categories:
    - Technical
tags: 
    - Node
    - Python
    - Javascript
    - NodeJS
---
I have written a number of scripts that access the Lex Machina API. Some of these were for testing, some for demo and some for proof of concepts for current and potential customers. As I look at the structure of them, almost of all of them fit into a distinct pattern.

The logic I have authored has these phases:

1. Optional search (input text, search for judge, party, etc) or possibly looping over a list (all state or federal district courts)
1. Using either that input and/or hardcoded values, do a query for cases
1. Take the resulting list of cases and look them up one by one
1. Extract values from individual cases
for use.

Quite often thus far, the uses I have for those extracted values are statistical. I am searching for the average length of time for something, or the sum of damages, or the most common occurrence of a value.

This pattern is so common in what I do as someone who understands the technical aspects but is a novice in the meaning of the legal that I wonder if there is any other kind of pattern? Is there a way to script the Lex Machina API that does not use a query as the framework from which everything else depends?

It does make sense in synchronization uses that one might skip the querying step. If your use of the API is to bring data into your matter management tool, you may already have the Lex Machina case ID of interest and you want to periodically check for updates with that case. When writing a standalone bit of logic, does that use case even exist that does not use a query?

Sometimes when I work with the API I am completely bounded by my imagination. When asked if a thing is possible, if that request is for information that exists in our API the answer is almost always "Yes, of course." However thinking of those use cases can be difficult for non-practictioners and those unfamiliar with how law firms and litigation funders operate.

Do you have a use case that differs from this design pattern? Do you have an out-of-the-box way to pursue logic with the data in the Lex Machina API? Let us know in the comments below. Our example code and even the design of our API is influenced by your input so speak up!

