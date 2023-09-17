Title: Software Project Estimation
Date: 2022-02-10 12:00:00
Modified: 2022-02-10 12:00:00
Category: 
Tags: 
Slug: 
Summary: 
Status: draft

KQL SYNTAX REFERENCE
https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/

- Lets you:
○ Investigate/analyze
○ Create alerts
○ Visualizations
○ ETL
- KQL > SQL, more concise, better optimized for ad-hoc query
- Different tools can utilize
○ Azure Data Explorer (SSMS like) - https://learn.microsoft.com/en-us/azure/data-explorer/kusto/tools/kusto-explorer
○ Azure Montior
○ Bunch of others
- Azure Monitor
○ Log Analytics tool lets you query against AM Logs store
- Azure Resource Graph
○ Azure Resource Management extension
○ Resource exploration, query across subscriptions to govern environment
○ Can access properties returned by resource providers more succinctly

- Query Structure
○ Data source, then conditions, ordering, filtering
- Type of Queries (query statement types)
○ Tabular expression statements
○ Let statements
- Tabular Expression
○ Input and output both tables/tabular datasets

- Let statements
○ Binding between name + expression
○ Can break queries into smaller named parts

- User-defined functions
○ Stored functions
    § Stored and managed schema entities
○ Query-defined functions
    § Within scope of a single query
