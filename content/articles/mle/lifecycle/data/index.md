---
title: "Data Stage"
date: 2022-02-25T11:50:54+03:00
weight: 10
---

# Data Stage

## Types of Datasets

**Small Data** vs. **Big Data**: generally, the threshold is "can a small team examine every single example 
in a reasonable time?".

{{< columns >}}
**Small Data**
- Every record can be manually examined
- Humans can label data
- Clean (true and consistent) labels are critical
- If the labels are inconsistent, it may be more worthy to fix that instead of collecting new data
and overcomplicate a model
<--->
**Big Data**
- Manual labeling is nearly impossible
- Focus of data processes
- **but** problems of rear events in Big Data are pretty similar to the problems of Small Data, where accurate 
labeling is critical
{{< /columns >}}

{{< columns >}}
**Unstructured Data**
- Humans can label more data
- Data Augmentation more likely to be helpful

<--->

**Structured Data**
- May be more difficult to obtain more data
- Human labeling may not be possible
{{< /columns >}}

### Examples

|            | Unstructured                                                | Structured                                                               |
|------------|-------------------------------------------------------------|--------------------------------------------------------------------------|
| Small Data | Manufacturing visual inspection  from 100 training examples | Housing price prediction based on  square footage, etc. from 50 examples |
| Big Data   | Speech recognition from 50 million examples                 | Online shopping recommendations for 1 million users                      |

## Label Consistency

Techniques:
- **Standardizing**: make an agreement between MLE, Subject Matter Experts and labelers. As well-defined as posible.
- **Merging Classes**: sometimes it's more productive to treat some classes as one 
(e.g. "small scratch" and "deep scratch" -> "scratch")
- **Unknown/Borderline Class**: introduce a separate class for ambiguous examples

To verify label consistency, the same data can be re-labeled by a few labelers or even by the same labeler 
after some time.   

## Ground Truth Definition

It is critical to understand how is the Ground Truth defined. How objective it is? 

When the GT is externally defined, HLP (Human Level Performance) gives an estimate of irreducable error. 
But if the GT is defined by a human's decision, it is the algorithm accuracy is generally "how close it is 
to the human's opinion".

## Obtain New Data

The earlier you start to iterate through [model training cycle]({{< ref "modeling#training-cycle" >}}) - the better. 

Brainstorm list of data sources:
| Source                 | Amount      | Cost   | Time |
|------------------------|-------------|--------|------|
| Owned                  | 100 units   | $0     | 0    |
| Crownsourced           | 1000 units  | $10000 | 14d  |
| Pay for labels         | 100 units   | $6000  | 7d   |
| Purchase data          | 1000 units  | $10000 | 1d   |
  

{{< hint warning >}}
Don't increase the dataset size more than 10x at a time. 
Otherwise, it can be really hard to predict how it will affect the model
{{< /hint >}}

## Data Provenance and Data Linage

**Data Provenance**: where the data comes from.  
**Data Linage**: how to reproduce the same data through sequence of steps.



