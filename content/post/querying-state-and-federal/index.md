---
title: "How Queries Differ between State and Federal"
date: 2023-06-07T10:21:14-04:00
description: "Federal district and state queries are similar in structure but not identical. Here is a discussion of the differences."
lead: "Federal district and state queries are similar in structure but not identical. Here is a discussion of the differences."
draft: true
categories:
    - Technical
tags: 
    - Queries
    - State Data
    - Federal Data
---

As of general availability, data from both federal district and state cases can be queried via the Lex Machina API. There are full articles on the developer portal about each type of query. Here is the one for [federal district queries](https://developer.lexmachina.com/default/docs/query_usage_portal_post) and one for [state queries](https://developer.lexmachina.com/default/docs/state_query_usage).

For this blog post, I will provide a very quick high level summary of the differences. For details in using either query, see the above articles.

# State Queries Need States

This may seem superfluous, but it isn't. As it stands, you can not presently mix states in queries. If you want to query for both Texas and Georgia cases, you need to perform two queries, each with the appropriate state constraint.

In the federal district query, you can include or exclude courts in an array such as:

```json
{
	"courts": {
		"include": ["njd","dcd"]
	}
}
```

In state, this becomes a mandatory field that defines the state being queried and optionally includes or excludes courts within that state. It does not make sense to use excludes if also using includes, because once including any court any other court not referenced is de facto excluded

```json
{
  "courts": {
    "state": "TX",
    "include": [
      "Fort Bend County District Court",
      "Harris County Court"
    ]
  }
```

In both cases, the list of valid courts can be obtained from the [/list-courts/{court_type} endpoint](https://developer.lexmachina.com/default/documentation/lexmachina-ga#/List/list_courts_list_courts__court_type__get) by using either "FederalDistrict" or "State" as the path parameter.

# Constraints that Differ Between Federal District and State

These are covered in greater depth in the state query article, but here is a list of constraints that differ:

## Not in State

    - magistrates
    - remedies 
    - findings
    - patents
    - mdl

## Only in State
    - rulings

## In Both but Different Structure
    - damages


# Conclusion

For most of the constraints available to query data in the Lex Machina API, the federal district and state queries work the same. It is worth exploring the various list endpoints in the API as those will present the full catalog of valid input into queries. Although these don't change often, they do change. New state and federal court coverage is added over time. Tags and categories can change. For example, "COVID-19" was not a case tag 4 years ago for obvious reasons.

This should give you a little taste of the queries we have available now in the Lex Machina API. Dig in as you can, and happy exploring!