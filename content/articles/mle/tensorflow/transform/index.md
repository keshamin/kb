---
title: "TensorFlow Transform"
date: 2022-03-15T13:40:36+03:00
---
# TensorFlow Transform

![ft_transform](tf_transform.png)

- **ExampleGen** splits dataset
- **StatisticsGen** calculates statistics per feature
- **SchemaGen** infers the types of features 
- **ExampleValidator** checks for data anomalies
- **Transform** performs feature engineering

{{< columns >}}
**Transform Inputs**
- Data
- Schema
<--->
**Transform Outputs**
- Transformed Data
- Transform Graph
{{< /columns >}}

The result **transform graph** (tf.Graph) holds all necessary constants and transformations. The same chain of transformations 
can be easily applied at serving time.

## Analizers Framework

Analizers:
- Scaling
  - scale_to_z_score
  - scale_to_0_1
- Bucketizing
  - quantiles
  - apply_buckets
  - bucketize
- Vocabulary
  - bag_of_words
  - tfidf
  - ngrams
- Dimensionality Reduciton
  - pca



