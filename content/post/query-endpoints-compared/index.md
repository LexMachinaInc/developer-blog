---
title: "Comparing the Query Endpoints"
authors: [Dave Slusher]
date: 2023-11-30T14:00:00-04:00
draft: false
description: "The Lex Machina API has three query endpoints. Here is a comparision of them."
lead: "The Lex Machina API has three query endpoints. Here is a comparision of them."
categories:
    - Technical
tags: 
    - Federal District
    - State
    - Appeals
    - Queries
---
Now that there are three different ways to query the Lex Machina API, knowing what aspects can be queried in each of the three is becoming a more complex task. This post is an attempt to put a lot of data on screen quickly with no real discussion. To see in depth discussions of each, look at the documentation in the developer portal for querying [district cases](https://developer.lexmachina.com/default/docs/query_usage_portal_post), [state](https://developer.lexmachina.com/default/docs/state_query_usage) and [appeals](https://developer.lexmachina.com/default/docs/appeals_query_usage).

The following tables represent which of the endpoints that concept exists in and can be queried. Whether the values are IDs, strings, tuples or complex JSON objects can be found above. This is just for the basic concepts existing, not a how-to. 

Also note that for shorthand in the particpant table, a value existing means both the include and exclude criteria exists for all of law firms, attorneys and parties. 

## Judges

|Query Constraint|Federal District|State|Appeals|
|---|------|------|-----|
|Judge| x | x | x |
|Magistrate| x |  |  |

## Participants

|Query Constraint|Federal District|State|Appeals|
|---|------|------|-----|
|Law Firms / Attorneys / Parties include/exclude| x | x | x |
| Plaintiff| x | x | | 
| Defendant |x| x| |
| ThirdParty | x| x| x|
| Appellant| | | x|
| Appellee| | | x|
| Respondent| | | x|
| PetionerMovant| | | x|


## Case Attributes

|Query Constraint|Federal District|State|Appeals|
|---|------|------|-----|
|Case Types| x | x | via OriginatingDistrictCaseCriteria |
|Case Tags| x | x | x |
|Resolutions| x | x | x |
|Findings| x |  |  |
|Remedies| x |  |  |
|Damages| x | x |  |
|Events| x | x |  |
|Rulings|  | x |  |
|Patents| x |  |  |
|MDL| x |  |  |

## Dates

|Date Constraint|Federal District|State|Appeals|
|---|------|------|-----|
|Filed| x | x | x |
|Terminated| x | x | x |
|Trial| x | x |  |
|Last Docket| x | x | x |

Courts exist in all three queries however they are all different and thus are not valuable to present in a table. It is worth noting that appeals has both a court specifier for the appeals court but also can reference the court of the original case via the OriginatingDistrictCaseCriteria. 

There are many similarities and many differences amongst all these queries. While it can be confusing at first, with a little care and attention all queries can be crafted and even somewhat reused across the endpoints.

Good luck and happy querying.