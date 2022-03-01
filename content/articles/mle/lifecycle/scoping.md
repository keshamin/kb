---
title: "Scoping Stage"
date: 2022-02-25T16:48:37+03:00
weight: 5
---

# Scoping Stage

Always separate a business problem from a technical solution.

Scoping Process:
{{< mermaid >}}
flowchart TD
BP(Brainstorm business problems)
AIS(Brainstorm AI solutions)
ASS(Assess the feasibility and value)
MIL(Determine milestones and budget)
BP --> AIS
AIS --> ASS
ASS --> MIL
{{< /mermaid >}}

## Milestones & Resourcing

Key specifications:
- ML metrics (accuracy, precision/recall, ...)
- Software metrics (latency, throughput, ...)
- Business metrics (revenue, ...)
- Resources needed (data, personnel, help from other teams, ...)
- Timeline

If unsure, consider benchmarking to other projects, or building a PoC first.
