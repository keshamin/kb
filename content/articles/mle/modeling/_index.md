---
title: "Modeling"
date: 2022-03-28T17:50:36+03:00
draft: false
---

# Modeling

## Hyperparameters Tuning

**Neural architecture search (NAS)** is a technique for automating the design of artificial neural networks. 

{{< columns >}}

**Trainable paramters**
- learned by the algorithm during taining
- e.g. weights of a neural network

<--->

**Hyperparameters**
- set before launching the training
- not updated by the training itself
- e.g. learning rate, number of units in a dense layer

{{< /columns >}}

Even in a small algorithm the number of tunable hyperparameters can be significant. So the **automation is key**.

Example framework for automated tuning is Keras Tuner. 
