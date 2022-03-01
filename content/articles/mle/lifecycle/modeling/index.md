---
title: "Modeling Stage"
date: 2022-02-24T13:29:29+03:00
weight: 15
---

# Modeling

{{< html >}}
<span style="font-famili: Calibri; font-size: 2em;">
    AI system = Code + Data
</span>
{{< /html >}}

Approaches to modeling
- Model-centric: improve the algorithm
- Data-centric: improve the data quality

## Training Cycle

{{< mermaid >}}
flowchart LR
MHD(Model \n + Hyperparameters \n + Data)
TR(Training)
EA(Error Analysis)
MHD --> TR
TR --> EA
EA --> MHD
{{< /mermaid >}}


## Why Low Average Error isn't Good Enough

Typical ML model challenges: 
1. Perform well on training dataset (avg training error)
2. Perform well on dev/test sets
3. Perform well on **business metrics/project goals**.  
In most cases, this is not the same as item #2. 

### Priorities
The model performance is measured by average error metrics over all possible requests. 
But in real world requests have priorities. So-called "disproportionally important" requests. 
From business perspective, the model performance requirements on such requests are higher. 

> Example:
> 
> In web search engine there are requests like: "Apple pie recipe" or "Latest movies". 
> They are Informational and Transactional queries. Most likely, there's no "best apple pie recipe", so 
> errors in ranking are forgivable.
> 
> In contrast, if user queries "YouTube" or "Reddit" they expect the correct result to be Top-1. 
> Such queries are Navigational and have higher error cost.

### Performance on Key Slices

Make sure to treat all slices of the dataset fairly.
The model **must not discriminate** by gender, location, ethnicity or other protected attributes.

### Rare Classes

Skewed data distribution:
- 99% negative
- 1% positive

If some class is rare the model can just ignore it without a major effect on average accuracy. 

To detect such a skew dataset the **Confusion Matrix** should be used instead of Accuracy.

{{< katex >}}
Precision = \cfrac{TP}{TP + FP} \qquad Recall = \cfrac{TP}{TP + FN}
{{< /katex >}}

Combining Precision and Recall - F1 score

{{< katex >}}
F_1 = \cfrac{2}{\cfrac{1}{Precision} + \cfrac{1}{Recall}}
{{< /katex >}}

## Establishing a Baseline Level of Performance

Baseline helps indicate what might be possible. In some cases it also gives a sense of what 
is irreducable error (Bayes error). A baseline can be established per category.

Ways to establish a baseline:
- Human Level Performance (HLP)
- Search for results of similar projects
- Quick-and-dirty implementation
- Performance of older system

## Error Analysis

By manually expecting misclassified examples you may come up with additional attributes/tags that should be assigned
to records in a dataset.
For example, you found out that some audio clips have car noises in the background. Maybe it's worth to add this column
to the dataset and check:
- what fraction of errors has that tag?
- Of all data with that tag what fraction is misclassified?
- What fraction of all the data has that tag?
- How much room for improvement is there on data with that tag?

Baseline helps indicate how much room for improvement is there for certain category:  
(Baseline accuracy - Current accuracy) * Category frequency.

For categories you want to prioritize:
- Collect more data
- Use augmentation to get more data
- Improve data quality

## Data Manipulations for Improving Performance

### Data Augmentation

The goal is to create **realistic** examples that:
1. the algorithm does poorly on
2. humans (or other baseline) do well on

As a rule, Data Augmentation does not hurt the performance if:
- the model is large (low bias)
- The mapping x -> y is clear (1 vs I)

Data Augmentation is a good fit **for unstructured data**.

### Adding features

For **structured data** it's often more efficient to add new features to existent data instead of 
creating completely new data records.

## Experiment Tracking

Things to track:
- Algorithm version
- Dataset used
- Hyperparameters
- Results

Desirable Features:
- Experiment reproducability
- Experiment results with metrics analysis
- Perhaps: resource consumption, visualization, etc...
