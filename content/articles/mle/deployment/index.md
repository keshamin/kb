---
title: "Model Deployment"
date: 2022-02-22T15:55:39+03:00
weight: 2
description: Introduction to Model Deployment issue.
---

# Model Deployment

## Key Challenges

{{< columns >}}

### ML/Statistics Issues

1. **Data Drift**:
Input data evolved and a trained model does not interpret it properly anymore

2. **Concept Drift**:
The "rules" of taking the decision evolved

<--->

### Software Engineering Issues

1. Realtime or Batch
2. Cloud or Edge
3. Resources Requirements
4. Latency/Throughput requirements
5. Logging
6. Security and Privacy

{{< /columns >}}


## Common Deployment Cases

1. New product
2. Automate/assist with manual task
3. Replace previous ML system


## Deployment modes

1. Shadow mode 
   - ML system works in parallel with current solution (manual or previous automated system)
   - ML system's decisions are not taken into account at this point
   - Monitoring system compares results from both systems to estimate accuracy and probably collect more training data
2. Canary deployment
   - ML system works in parallel with current solution
   - New system handles a small portion of traffic, e.g. 5%
   - If there's no degradation, the portion is gradually increased
3. Blue/Green Deployment
   - ML system works in parallel with current solution
   - At some point a router in front of both systems switches all the traffic to the new system
   - In case of degradation, the rollback is easy


## Degree of Automation

{{< mermaid >}}
flowchart LR
HO[/Human Only/]
SM[/Shadow Mode/]
AA[/AI Assistance/]
PA[/Partial Automation/]
FA[/Full Automation/]
HO---SM---AA---PA---FA
{{< /mermaid >}}

"Human in the loop" deployments:
- **AI Assistance**: ML System highlights interesting input, but the decision is still taken by human
- **Partial Automation**: the decisions are taken by the ML System, but if it is not sure, 
it forwards the request to human. The approach if very useful to collect more training data 
when the accuracy is not good enough.


## Monitoring

To build a monitoring dashboard:
- Brainstorm the things that could go wrong
- Define the metrics that would reflect these problems

{{< hint info >}}
It is OK to start with a big number of metrics and remove some of them as you understand which are not representative.
{{< /hint >}}

### Examples of Metrics

{{< columns >}} <!-- begin columns block -->
#### Software Metrics
- Memory
- Compute
- Latency
- Throughput
- Server Load

<---> <!-- magic separator, between columns -->

#### Input Metrics
- Number of missing values
- Avg input audio length/volume
- Avg image brightness

<--->

#### Output Metrics
- Average output value
- Number of NULLs in output
- Number of times user retries the same request
- Number of times user refuse to use the system
{{< /columns >}}

