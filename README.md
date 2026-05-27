# Erdgeist — Resilient Vector Search under GPU Heterogeneity and Partial Failures

> *"In Lebensfluten, im Tatensturm wall ich auf und ab, webe hin und her!"*
> — Erdgeist, Faust I

The Earth Spirit is indestructible — Erdgeist's vector index survives
partial GPU failures via heterogeneity-aware replica placement and
graceful degradation across A6000 ×2 + H100 ×1 + CPU.

## Upstream

| Directory | Origin | Role |
|-----------|--------|------|
| `upstream/vsag` | [antgroup/vsag](https://github.com/antgroup/vsag) | Graph-based ANN index engine |
| `upstream/bigvectorbench` | [BenchCouncil/BigVectorBench](https://github.com/BenchCouncil/BigVectorBench) | Fault-injection eval framework |

## Fault Model

```
Normal:                Degraded (H100 fail):   Degraded (A6000 fail):
┌──────┐ ┌──────┐     ┌──────┐ ┌──────┐       ┌──────┐ ┌──────┐
│ H100 │ │A6000 │     │ ████ │ │A6000 │       │ H100 │ │ ████ │
│primary│ │replica│     │ FAIL │ │promote│       │ full │ │ FAIL │
└──────┘ └──────┘     └──────┘ └──────┘       └──────┘ └──────┘
```
