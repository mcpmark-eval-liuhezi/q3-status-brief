# The Paper That Started the AI Trade — Thematic Briefing

Working title: *The Paper That Started the AI Trade* — NVIDIA (NVDA) as the company at the center of the AI build-out, anchored on the transformer paper "Attention Is All You Need" (arXiv:1706.03762).

## 1. Company Snapshot — NVIDIA (NVDA)

- **Sector / Industry:** Technology / Semiconductors
- **Market cap:** 4078186790912 USD (4.08 trillion, as returned by the data service); non-diluted market cap 4078186830000 USD
- **Current price:** 168.89 USD (previous close 178.67; 52-week range 164.27 - 243.37)
- **Institutional ownership:** heldPercentInstitutions 0.71384 (institutions hold 0.74364 of the float); institutionsCount 7753; insider holding (heldPercentInsiders) 0.04006
- **Business profile:** Data center scale AI infrastructure company; two segments — Compute & Networking (data center accelerated computing, networking, AI platforms) and Graphics (GeForce GPUs, Quadro/RTX for enterprise workstations). ~42000 full-time employees; incorporated 1993; HQ Santa Clara, CA. CEO Jen-Hsun (Jensen) Huang.
- **Financials (as reported):** revenue growth 1.059, profit margin 0.63663, trailing EPS 7.91, trailing P/E 21.35, forward P/E 10.60, revenue ~302.97B USD TTM, free cash flow ~41.81B USD, strong buy consensus (recommendationMean 1.32258, 57 analyst opinions).

## 2. Institutional Ownership Table

| Holder | Shares Reported | % Held (pctHeld) | Value (USD) | % Change | Date Reported (epoch ms) |
|---|---|---|---|---|---|
| Blackrock Inc. | 1941918386 | 0.0806 | 327970595026 | 0.0085 | 1782777600000 |
| Vanguard Capital Management LLC | 1540816358 | 0.0639 | 260228473762 | 0.0015 | 1782777600000 |
| FMR, LLC | 1026051548 | 0.042600002 | 173289845315 | 0.0324 | 1782777600000 |

**Institutional context:** institutions hold 71.384% of shares outstanding (0.71384) and 74.364% of float (0.74364) across 7753 institutions; insiders hold 4.006%.

## 3. Paper Facts — "Attention Is All You Need" (arXiv:1706.03762)

**Headline machine-translation results (from abstract):**
- **28.4 BLEU** on the WMT 2014 English-to-German translation task — improving over existing best results, including ensembles, by over 2 BLEU.
- **41.8 BLEU** on the WMT 2014 English-to-French translation task — new single-model state-of-the-art, achieved after training for 3.5 days on eight GPUs, a small fraction of the training cost of the best models in the literature.

**Architecture (from the paper's Model Architecture section):**
- **Encoder:** stack of **N=6 identical layers**. Each layer has two sub-layers: multi-head self-attention + position-wise fully connected feed-forward network. Residual connection around each sub-layer followed by layer normalization — LayerNorm(x + Sublayer(x)). All sub-layers and embeddings produce dimension d_model = 512.
- **Decoder:** also a stack of **N=6 identical layers**. Each has three sub-layers: multi-head self-attention (masked to prevent attending to subsequent positions), encoder-decoder multi-head attention over the encoder output, and a position-wise feed-forward network. Same residual + layer normalization.
- **Scaled dot-product attention:** The paper calls its particular attention "Scaled Dot-Product Attention." Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V. Dot products are divided by sqrt(d_k); the paper notes that for large d_k the dot products grow large in magnitude, pushing the softmax into regions with extremely small gradients, so the dot products are scaled by 1/sqrt(d_k).
- **Multi-head attention:** Queries, keys and values are linearly projected h times with different learned linear projections; attention is performed in parallel on each projected version, outputs are concatenated and projected again. The base model uses **h=8 parallel attention heads**, with d_k = d_v = d_model/h = 64. Total computational cost is similar to single-head attention with full dimensionality.

## Sources

- Paper: **arXiv 1706.03762** — "Attention Is All You Need" (Vaswani et al.); facts above verify results (BLEU 28.4 EN-DE / 41.8 EN-FR), encoder-decoder stacks of N=6 layers, scaled dot-product attention with 1/sqrt(d_k) scaling, and h=8 multi-head attention, as stated in the paper's abstract and Model Architecture section.
- Market data: Yahoo Finance data service — NVDA stock info and institutional holder data (most recent reporting date as returned by the service: epoch 1782777600000).
