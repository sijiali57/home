---
layout: post
title: "Liquibase MD5SUM Checking Failed"
date: 2022-3-4
categories:
  - DataBase
tags:
  - Liquibase
  - Big Data
---

## Liquibase MD5SUM Error

In the recently project releasing, the deployment job failed due to the Error message from Liquibase -

```
Checking Liquibase status failed: [timestamp] INFO [liquibase.integration] No Liquibase Pro license key supplied. Please set liquibaseProLicenseKey on command line or in liquibase.properties to use Liquibase Pro features.\n[timestamp] INFO [liquibase.servicelocator] Cannot load service: liquibase.parser.ChangeLogParser: liquibase.parser.core.json.JsonChangeLogParser Unable to get public no-arg constructor\n[timestamp] INFO [liquibase.servicelocator] Cannot load service: liquibase.parser.ChangeLogParser: liquibase.parser.core.yaml.YamlChangeLogParser Unable to get public no-arg constructor\n[timestamp] INFO [liquibase.changelog] Reading from database.DATABASECHANGELOG\n[timestamp] SEVERE [liquibase.integration] Unexpected error running Liquibase: Validation Failed:\n     1 change sets check sum\n          changelog/changeID/sqlchange.sql::changeID::author was: MD5SUM value but is now: different MD5SUM \n\nliquibase.exception.ValidationFailedException: Validation Failed:\n     1 change sets check sum\n
```

During this release, there is no any changes for this repo, so it's very odd to get this check sum failure.

In order to understand this error, I google what is MD5SUM value and how does value be used inside Liquibase.

## What is MD5SUM

Liquibase use a table DATABASECHANGELOG to track all the changes. Inside this table, there is a column called "MD5SUM". Liquibase use this value to check is there a new change inside this database - changeSet. If the orginal changeLog value has been changed, then the MD5SUM value will be different than the original one, and during the Liquibase setup, it will return the above error.

## Solution for this Error

Solution 1 - If you have liquibase command in your Machine

then just simply fun "mvn liquibase:clearCheckSums" - https://docs.liquibase.com/tools-integrations/maven/commands/maven-clearchecksums.html

Solution 2 - Manually update the MD5SUM values

```
UPDATE DATABASECHANGELOG SET MD5SUM=null WHERE ID='XXX';
```
