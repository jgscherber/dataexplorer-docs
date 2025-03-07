---
title: .alter table update policy command - Azure Data Explorer
description: This article describes the .alter table update policy command in Azure Data Explorer.
services: data-explorer
author: orspod
ms.author: orspodek
ms.reviewer: yonil
ms.service: data-explorer
ms.topic: reference
ms.date: 10/10/2021
---
# .alter table update policy

Change the table update policy. The [update policy](updatepolicy.md) instructs Azure Data Explorer to automatically append data to a target table whenever new data is inserted into the source table, based on a transformation query that runs on the data inserted into the source table.

> [!NOTE]
> The source table and the table for which the update policy is defined must be in the same database.
> The update policy function schema and the target table schema must match in their column names, types, and order.

## Syntax

`.alter` `table` *TableName* `policy` `update` *ArrayOfPolicyObjects*
`.alter` `table` *DatabaseName*`.`*TableName* `update` *ArrayOfPolicyObjects*

## Arguments

-*DatabaseName* - Specify the name of the database.
*TableName* - Specify the name of the table. Use without *DatabaseName* when running in the required database's context. A wildcard (*) denotes all tables.
*ArrayOfPolicyObjects* - An array with one or more policy objects defined.

## Returns

Returns a JSON representation of the policy.

## Example

Change the update policy for a table:

```kusto
.alter table MyDatabase.MyTable policy update @'[{"IsEnabled": true, "Source": "MyTableX", "Query": "MyOtherTable", "IsTransactional": true, "PropagateIngestionProperties": false}]'
```
