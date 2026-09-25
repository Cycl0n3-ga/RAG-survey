---
paper_id: "Hsieh2024_RULER"
title: "RULER: What’s the Real Context Size of Your Long-Context Language Models?"
authors:
  - "Cheng-Ping Hsieh"
  - "Simeng Sun"
  - "Samuel Kriman"
  - "Shantanu Acharya"
  - "Dima Rekesh"
  - "Fei Jia"
  - "Yang Zhang"
  - "Boris Ginsburg"
year: 2024
publication_year: 2024
venue: "COLM 2024"
doi: null
arxiv: "2404.06654"
url: "https://openreview.net/forum?id=kIoBbc76Sy"
pdf_file: "Papers/06 - Benchmarks & Evaluation/(arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models.pdf"
tags:
  - paper
  - benchmark
  - long-context
  - effective-context-length
verification_status: "verified"
last_verified: 2026-09-26
artifact_type: "benchmark_paper"
research_questions:
  - "effective_context_length"
  - "long_context_utilization"
benchmark_ids:
  - "RULER"
metrics:
  - "Average Accuracy"
  - "Effective Context Length"
taxonomy_version: "v2"
taxonomy_home: "A01"
primary_domain: null
secondary_domains:
  - "D13"
paradigm_tags:
  - "long_context_evaluation"
adjacent_interfaces:
  - "A01"
---

# RULER: What’s the Real Context Size of Your Long-Context Language Models?

## 一話摘要

RULER 擴充單一 Needle-in-a-Haystack，加入 multi-needle retrieval、multi-hop tracing、aggregation 與 QA。論文測試 17 個 long-context LMs、13 個 tasks；雖然所有模型都宣稱至少 32K context，只有約一半在 32K 仍維持作者設定的 satisfactory-performance threshold。

## Benchmark Design

四類 tasks：

1. Retrieval
2. Multi-hop Tracing
3. Aggregation
4. Question Answering

測試長度為 4K / 8K / 16K / 32K / 64K / 128K，每個 task / length 使用 500 個 generated examples。

## Effective Context Length

作者把 Llama2-7B 在 4K 的 average performance 85.6% 當 threshold：

- 模型在某長度的 13-task average accuracy 高於 85.6%，該長度才算有效；
- effective context length 是仍通過 threshold 的最大測試長度。

這不是通用的「85% industry standard」，只是本 paper 的 operational definition。

## 主要結果 — Table 3

| Model | Claimed | Effective |
|---|---:|---:|
| Gemini-1.5-Pro | 1M | >128K |
| GPT-4 | 128K | 64K |
| Llama3.1 70B | 128K | 64K |
| GLM4 9B | 1M | 64K |
| Qwen2 72B | 128K | 32K |
| Command-R-plus | 128K | 32K |
| Llama3.1 8B | 128K | 32K |
| Yi 34B | 200K | 32K |
| GradientAI/Llama3 70B | 1M | 16K |
| LWM 7B | 1M | <4K |

正確結論：
- 幾乎所有模型都隨 context 增長而下降；
- 多數 effective length 小於 advertised length；
- 但不能說「幾乎所有 128K 模型在 32K 前崩掉」，因為 GPT-4、Llama3.1-70B 等達 64K，Gemini-1.5-Pro 在測試範圍內 >128K。

## Limitations

- synthetic tasks 為主；能控制難度，但不等同真實應用能力。
- effective-length threshold 是 paper-specific。
- RULER 主要是 A01 long-context benchmark，不是完整 RAG benchmark。

## 對本專案的意義

適合測試「不 retrieval、直接長 context read」是否真的可靠；不能替代 D05/D06/D09 的 retrieval / evidence / grounding evaluation。

## Sources

- COLM 2024: https://openreview.net/forum?id=kIoBbc76Sy
- arXiv: https://arxiv.org/abs/2404.06654
- [[Papers/06 - Benchmarks & Evaluation/(arXiv 2024-04) RULER - What is the Real Context Size of Your Long-Context Language Models.pdf|Local PDF]]
