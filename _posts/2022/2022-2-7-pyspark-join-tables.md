---
layout: post
title: "Pyspark join tables"
date: 2022-2-7
categories:
  - PySpark
tags:
  - PySpark
  - Python
  - Big Data
---

**Use case**
Similar with SQL - JOIN


```
from pyspark.sql import DataFrame
from pyspark.sql.functions import count, avg
import pyspark.sql.functions as F

df_left.join(df_right, df_left.joinKey == df_right.joinKey, "inner")\
            .select('df_left.*','df_right.selectColumn')\
        .collect()

```
