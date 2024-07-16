---
title: Specific findings
date: 2024-06-14T08:00:00-07:00
draft: false
description: Specific findings in class action cases & changes to patent invalidity
lead: Specific findings in class action cases & changes to patent invalidity
authors: [Justin Brownstone]
categories:
    - News
tags: 
    - Schema
    - Federal District
---
We recently made a change to the schema for both Class Action cases and involving Patent Invalidity. Previously, in Class Action cases, the API for a given case returned only the general class action finding, such as “Class Certification: Deny,” and not the specific findings associated with the overall decision of whether to deny or grant class certification. Consequently, the schema was modified so that Class Action cases now return the following specific findings if relevant:

* No 23(b)(3) Predominance and Superiority
* No 23(a)(2) Commonality
* No 23(a)(3) Typicality
* No 23(a)(4) Adequate Representation
* Other Rule 23 Denial
* No 23(a)(1) Numerosity
* No Ascertainable Class
* No Class Representative Standing

We have also made a corresponding change to how cases display the specific findings of patent invalidity. Previously, these findings were listed under “patentInvalidity reasons.” In order to create consistency across case types, we now display both the specific reasons for class action findings and the specific reasons for patent invalidity findings under the “specificReasons” field.