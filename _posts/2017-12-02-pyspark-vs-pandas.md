---
layout: post
title: Pyspark vs Pandas
description: "" 
tags: [big data]
categories: [TIL]
---

## PySpark vs Pandas

Spark and Pandas DataFrames are very similar.

```python
# Pandas

# load data
df = pd.read_csv("mtcars.csv")

# view dataframe
df 
df.head(10)

# columns and data types
df.columns
df.dtypes

# rename columns
df.columns = ['a', 'b', 'c']
df.rename(columns = {'old': 'new'})

# drop column
df.drop('mpg', axis=1)

# filtering
df[df.mpg < 20]
df[(df.mpg < 20) & (df.cyl == 6)]

# add column
df['gpm'] = 1 / df.mpg # division by 0 gives inf

# fill nulls
df.fillna(0) # more options than PySpark has

# aggregation
df.groupby(['cyl', 'gear']) \
  .agg({'mpg':'mean', 'disp':'min'})
```

```python
# PySpark

# load data
df = spar.read \
  .options(header=True, inferSchema=True) \
  .csv("mtcars.csv")

# view dataframe
df.show() # df represents a schema
df.show(10)

# columns and data types
df.columns
df.dtypes

# rename columns
df.toDF('a', 'b', 'c')
df.withColumnRenamed('old', 'new')

# drop column
df.drop('mpg')

# filtering
df[df.mpg < 20]
df[(df.mpg < 20) & (df.cyl == 6)]

# add column
df.withColumn('gpm', 1 / df.mpg) # division by 0 gives null

# fill nulls
df.fillna(0)

# aggregation
df.groupby(['cyl', 'gear']) \
  .agg({'mpg':'mean', 'disp':'min'})
```

Okay. We get the point and now let's see what else is a little bit more diffrent.

```python
# Pandas

# STANDARD TRANSFORMATIONS
# uses python numpy lib
import numpy as np
df['logdisp'] = np.log(df.disp)

# ROW CONDITIONAL STATEMENTS
df['cond'] = df.apply(lambda r:
  1 if r.mpg > 20 else 2 if r.cyl == 6 else 3,
  axis = 1)

# PYTHON WHEN REQUIRED
df['disp1'] = df.disp.apply(lambda x: x+1)

# MERGE/JOIN DATAFRAMES
left.merge(right, on='key')
left.merge(right, left_on='a', right_on='b')

# PIVOT TABLE
pd.pivot_table(df, values='D', \
  index=['A', 'B'], columns=['C'], \
  aggfunc=np.sum)

# SUMMARY STATISTICS
df.describe()

# HISTOGRAM
df.hist()

# SQL
n/a
```

```python
# PySpark

# STANDARD TRANSFORMATIONS
# uses built-in functions 
import pyspark.sql.functions as F
df.withColumn('logdisp', F.log(df.disp))

# ROW CONDITIONAL STATEMENTS
df.withColumn('cond', \
  F.when(df.mpg > 20, 1) \
   .when(df.cyl == 6, 2 \
   .otherwise(3))
   
# PYTHON WHEN REQUIRED
from pyspark.sql.types import DoubleType
fn = F.udf(lambda x: x+1, DoubleType())
df.withColumn('disp1', fn(df.disp))

# MERGE/JOIN DATAFRAMES
left.join(right, on='key')
left.join(right, left.a == right.b)

# PIVOT TABLE
df.groupBy("A", "B").pivot("C").sum("D")

# SUMMARY STATISTICS
df.describe().show() # only count, mean, stddev, min, max

# HISTOGRAM
df.sample(False, 0.1).toPandas().hist()

# SQL
df.createOrReplaceTempView('foo')
df2 = spark.sql('select  * from foo')
```