---
title: "Lex Machina Client Libraries"
date: 2023-06-23T10:00:00-04:00
draft: false
description: "You can install client libraries for Python and JavaScript to simplify accessing the Lex Machina API"
lead: "You can install client libraries for Python and JavaScript to simplify accessing the Lex Machina API"
categories:
    - Technical
tags: 
    - Releases
    - Python
    - JavaScript
    - Node
toc: false
---
As of now, the Lex Machina API has client libraries published for both Node and Python. In this article, I will walk through the installation, configuration and use of both.

# Installation

Both libraries are published to their respective package directories. 

## Node

The Node package is [published to npm](https://www.npmjs.com/package/@lexmachina/lexmachina-client). To install it in your project directory use this command:

```bash
npm install @lexmachina/lexmachina-client
```

## Python

The Python package is [published to PyPi](https://pypi.org/project/lexmachina-client/). To install it in your Python environment use this command: 

```bash
pip install lexmachina-client
```

# Configuration

For the contents of the configuration file for either client, you will use the CLIENT_ID and CLIENT_SECRET of the credentials for your application. Directions on how to generate credentials [are on the developer portal](https://developer.lexmachina.com/default/docs/generating_oauth_credentials).

## Node

For the node package, in your project directory create a subdirectory named "config" . Inside that directory create a file named "config.json". By default this will be the config file used unless you specify a different one in the constructor. Use the below values:

```json
{
    "baseURL": "https://api.lexmachina.com",
    "authParams": {
        "client": {
            "id": "CLIENT ID",
            "secret": "CLIENT SECRET"
        },
        "auth": {
            "tokenHost": "https://api.lexmachina.com",
            "tokenPath": "/oauth2/token"
        }
    }
}
```

## Python

For the python package, in your project directory create a subdirectory named "config" . Inside that directory create a file named "config.ini". By default this will be the config file used unless you specify a different one in the constructor. Use the values below:

```ini
[URLS]
token_url = /oauth2/token
base_url = https://api.lexmachina.com

[CREDENTIALS]
client_id = "CLIENT_ID"
client_secret ="CLIENT_SECRET"
```

# Instantiating a Client Object

## Node

To use the API via the Node client you instantiate a client object. If no parameter is passed, it will use the file /config/config.json (relative to execution path) created above.

```javascript

const LexMachinaClient = require("@lexmachina/lexmachina-client")

var client = new LexMachinaClient();
```
Once the client is instantiated, you can call any of the methods that exist. [The NpmJS page has a list of all methods available](https://www.npmjs.com/package/@lexmachina/lexmachina-client).


## Python

To use the API via the Python client you instantiate a client object. If no parameter is passed, it will use the file /config/config.ini (relative to execution path) created above.

```python
from lexmachina import LexMachinaClient

client = LexMachinaClient()
```
Once the client is instantiated, you can call any of the methods that exist. [The PyPi page has a list of all methods available](https://pypi.org/project/lexmachina-client/).


# Querying

For both clients, to query you first instantiate a query object and then add constraints. These constraints can be chained together for convenience. Once specified, the query object is passed to the client to execute the query.

## Node 

```javascript
const { LexMachinaClient, DistrictCasesQueryRequest } = require("@lexmachina/lexmachina-client")

var districtQuery = new DistrictCasesQueryRequest();
districtQuery.setDate('2021-01-01',"filed", "onOrAfter")
.setDate('2021-12-31', "filed", "onOrBefore")
.addCaseTypesInclude("Bankruptcy")
.setCaseStatus("Terminated");

var cases =  client.queryDistrictCases(districtQuery, { pageThrough: true })
```
At this point ```cases``` contains a list of the district case IDs that match the query and can be looked up individually.

## Python 

```python
from lexmachina import DistrictCaseQueryRequest

query = DistrictCaseQueryRequest()

case_query = query.set_date("2021-01-01", "filed", "onOrAfter").set_date("2021-12-31", "filed", "onOrBefore").include_case_types("Bankruptcy")

cases = client.query_district_case(case_query, {"pageThrough": True}, page_size=100)
```

At this point ```cases``` contains a list of the district case IDs that match the query and can be looked up individually.

# Conclusion

As you can see, the design of the two libraries is very similar. They mainly differ around the idiosyncracies of JavaScript vs Python and the conventions of each. In general they do the same thing in the same way.

This is just a very quick overview of what is available in the client packages. The developer portal has more information on the many details of [querying district cases](https://developer.lexmachina.com/default/docs/query_usage_portal_post) and also [state cases](https://developer.lexmachina.com/default/docs/state_query_usage). 

If you are interested in exploring the Lex Machina API please reach out. If you are current customer and need help with these or any other method of accessing our API, please feel free to email dslusher@lexmachina.com . 

Happy querying! Happy integrating! 