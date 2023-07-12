---
title: "Judgments by Day of the Week"
date: 2023-05-26T10:00:00-04:00
draft: false
description: "An example script for judgments by day of the week, inspired by a conversation at CLOC"
lead: "An example script for judgments by day of the week, inspired by a conversation at CLOC"
authors: [Dave Slusher]
categories:
    - Examples
tags: 
    - Queries
    - NodeJS
    - CGI at CLOC
---
Recently some of the Lex Machina product team went to Las Vegas to exhibit at [the CLOC Global Institute conference](https://events.cloc.org/event/1d32983d-33ab-47ff-a8ae-9994043fcd1f/summary). It was an interesting event at which we talked to a number of current and potential customers. One idea that was thrown out almost as a joke was the idea of using our API to determine for a given judge how they ruled on the day of the week. Of course, I took this as a challenge.

Note that this requires API access and the [node client package](https://www.npmjs.com/package/@lexmachina/lexmachina-client). The final script is [in our Github example repository](https://github.com/LexMachinaInc/node-lexmachina-api-client/blob/ga/examples/judge-day-of-week.js). I thought I would highlight a few bits of the logic. 

I have a function that I use to search for and return a single judge from command line input. Once I have that, the following query constraints are added:

```javascript

    query.addJudgesInclude(judge_id);
    query.setCaseStatus('Terminated');
    query.addEventTypesInclude('Summary Judgment');
    // Do the actual query
    var cases = await client.queryDistrictCases(query, { pageThrough: true });    
```

That gives an array of results that are iterated through. I added the "Summary Judgment" event type because that only includes cases that could be ended by a judge on a specific day. The goal is to see if there are statistical differences, so that gives a better picture.

In the loop, for each case the full information is fetched from the API then the array of events is pulled. 

```javascript
        var sjEvents = events.filter(event => event.type == 'Summary Judgment');
        var sjDate = sjEvents[0].occurred;
        var dayOfWeek = moment(sjDate).format('dddd');
        console.log('Summary judgment on %s which is %s  %s:%s', sjDate, dayOfWeek, resolution.summary, resolution.specific);
```

This snippet creates an array of the events that are the summary judgment itself via the JavaScript .filter() function. There will only be one, which is why it is dereferenced as [0]. [MomentJS](https://momentjs.com/) is then used to convert the date (found in the .occurred field) to the actual day of the week. Some other code (not shown here) is used to create an associative array to maintain the count of various decisions on days of the week. Because summary judgments can be on some but not all aspects of the case, some of these final resolutions include trial outcomes. The day of the week listed is the day the summary judgment was issued which may not have concluded all aspects of the case.

The final result is at the bottom of this post, run for federal judge Phillip Brimmer. Why him? Why not? While this example is a bit of a lark, it does represent the kind of analysis that can be performed with the Lex Machina data. The results don't make a statement of cause and effect, just the statistics of the outcomes. Perhaps a certain court only hears motions of a type on specific days of the week. Still, if you want to determine the probability of an outcome based on past data, you can always do it. This script is 82 lines all in, of which 30 are setup and getting the judge_id from the input. It does not take a lot of effort or code to do a data analysis with Lex Machina data - just an idea and a little time to code and run the script.



```

Summary for Philip A. Brimmer

For Likely Settlement:Likely Settlement
Wednesday: 30
Tuesday: 27
Monday: 23
Thursday: 22
Friday: 18
Sunday: 1

For Claim Defendant Win:Judgment as a Matter of Law
Tuesday: 1

For Claim Defendant Win:Summary Judgment
Monday: 34
Tuesday: 33
Wednesday: 25
Thursday: 23
Friday: 21
Saturday: 1

For Claimant Win:Trial
Friday: 5
Tuesday: 4
Wednesday: 3
Thursday: 3
Monday: 2

For Claimant Win:Summary Judgment
Thursday: 6
Monday: 5
Tuesday: 4
Wednesday: 3
Friday: 3

For Claimant Win:Consent Judgment
Monday: 1
Tuesday: 1
Friday: 1

For Procedural:Contested Dismissal
Monday: 5
Thursday: 4
Tuesday: 2
Wednesday: 2
Friday: 1

For Claim Defendant Win:Consent Judgment
Tuesday: 1
Wednesday: 1

For Claim Defendant Win:Trial
Friday: 5
Tuesday: 4
Monday: 2
Thursday: 1

For Claimant Win:Default Judgment
Wednesday: 2
Monday: 1
Thursday: 1

For Procedural:Multidistrict Litigation
Thursday: 5
Tuesday: 1
Wednesday: 1

For Procedural:Dismissal
Tuesday: 5
Thursday: 3
Monday: 1
Wednesday: 1

For Claim Defendant Win:Judgment on the Pleadings
Tuesday: 2
Wednesday: 2
Monday: 1
Thursday: 1

For Claimant Win:Judgment as a Matter of Law
Monday: 1

For Procedural:Consolidation
Thursday: 1
LNGHBEM-RH7P25734Y:API-Demos slusherd$
```
