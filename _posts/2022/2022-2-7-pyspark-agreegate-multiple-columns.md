---
layout: post
title: "Pyspark aggregate multiple columns"
excerpt: "Pyspark basic calculation"
date: 2022-2-7
categories:
  - PySpark
tags:
  - PySpark
  - Python
  - Big Data
---

**Use case**
Similar with SQL - GROUPBY, COUNT, COUNT(DISTINCT),SUM


```
from pyspark.sql import DataFrame
from pyspark.sql.functions import count, avg
import pyspark.sql.functions as F

def pyspark_agg(df: DataFrame) -> DataFrame:
    return df.groupBy(
                df.DateId,
                df.Country,
                df.Platform
            ).agg(count("Id").alias("NormalCounter"),
                  F.countDistinct("UserId").alias("UniqueUsersCounter"),
                  F.countDistinct("IP").alias("UniqueUsersLocationCounter")
                  )

```
