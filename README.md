# Elasticserach data analisys and visualisation for pokemon

Project Description: This is a visualisation of pokemon statistics for first to sixth generation. The idexing is setup via a csv file. 

## Setup

1. Installation: You need to download elasticserach and kibana from the elasticstack website:https://www.elastic.co/downloads/. Then take the data folders from the repositry and replace the local dirs with them. To run elasticsearch and kibana it is recomendet to have more than 10% free on diskspace and sufficient RAM(At least 8GB). 

2. Data Upload: To upload data first you need to create indexing. This can be done manualy trough kibana or done automaticaly when a file is uploaded. 

## Data Manipulation

1. Sorting and Corrections:  Due to the data being not 100% correct, edits were made using kibanas devtool and Json queries to make changes to existing data. Using kibana's devtool with JSON queries is easy and intuitive, and is like using Postman. 

Here is an example of the used JSON Quesries:
```
POST pokemon/_update_by_query
{
    "query":{
        "terms":{
            "Name.keyword": ["Arceus", "Mew", ...(A lot of mythical pokemon names)]
        }
    },
    "script": {
        "source": "ctx._source.Mythical = true",
        "lang": "painless:
    }
}
```
```
POST /your_index/_update_by_query
{
  "query": {
    "bool": {
      "must_not": {
        "exists": {
          "field": "your column name"
        }
      }
    }
  },
  "script": {
    "source": "ctx._source[\"your column name\"] = 'None'"
  }
}
```
## Search and Visualization

1. KQL Searches: In the Statistics discover part of kibana you can sort data using KQL filters. The KQL syntax is as follows: "<Column name><operator><value> <AND/OR>...". This syntax while simple can be used for complex filters to sort your data the way you need. This same syntax can be used on dashbords to source the source data. 

2. Statistical Visualizations: Kibana has a Dashboard which gives you the ability to visualise your data. The given tools allow for any data search and visualisation, including sorting which data is considered in the statistic. 

Shoutout to the elastic stack.
