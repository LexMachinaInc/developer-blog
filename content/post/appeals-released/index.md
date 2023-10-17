---
title: "Appeals API Released to Production"
authors: [Dave Slusher]
date: 2023-10-17T08:00:00-04:00
draft: false
description: "The Lex Machina API now has appeals court data"
lead: "The Lex Machina API now has appeals court data"
categories:
    - News
tags: 
    - Releases
---
As part of our efforts to continuously improve and expand the capabilities of the Lex Machina API, we now have Appeals data available via the API.

The in-app documentation has been updated to reflect the changes, new endpoints and the new inputs to some of the list endpoints. Any of the endpoints that previously took "FederalDistrict" or "State" as input now also take "FederalAppeals" as context for the list of resources requested.

The other big change is the addition of the /query-appeals-cases/  endpoint. This works analogously to the /query-district-cases/ and /query-state-cases/ in the JSON body format and the format of the returned data. There are some wrinkles in the query parameters as federal district, state and appeals have non-identical data on which to search. There will be further blog posts and articles in the developer portal to discuss the queries. 

For now, if this is information that you have been awaiting, it is now here. Your existing credentials and applications are able to access all new endpoints with no changes. All list endpoints now return the new data. You are free to hit them as you need.

As always, happy integrating and reach out if you need any assistance on your automation journey.

The Lex Machina Team