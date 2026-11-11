# The Paper That Started the AI Trade — Thematic Briefing (Draft)

Working title for research meeting. Facts below verified against Yahoo Finance (NVDA) and arXiv:1706.03762 on 2026-12-04. Commentary to be added separately.

## 1. Company Snapshot — NVIDIA (NVDA)

- **Company:** NVIDIA Corporation (NASDAQ: NVDA) | **Sector:** Technology | **Industry:** Semiconductors
- **Headquarters:** Santa Clara, California, United States
- **Market cap:** 4,078,186,790,912 (as returned by Yahoo Finance)
- **Current price:** 168.89 USD (NasdaqGS real-time)
- **Employees:** 42,000 full-time
- **Insiders held:** 0.04006 (4.006%) | **Institutions held:** 0.71384 (71.384%) | **Institutions as % of float:** 0.74364 (74.364%) | **Institutions count:** 7,753
- **Business model:** NVIDIA operates as a data center scale AI infrastructure company; segments are Compute & Networking and Graphics. Compute & Networking provides data center accelerated computing, networking platforms and AI solutions; Graphics offers GeForce GPUs and professional/workstation GPUs.
- **Key financials:** Trailing P/E 21.351454; forward P/E 10.6033; beta 2.247; profit margin 0.63663; revenue growth 1.059; earnings growth 1.278; dividend yield 0.59%; trailing EPS 7.91.

## 2. Institutional Ownership Table (as reported by Yahoo Finance)

All top holders reported as of 2026-06-30.

| # | Holder (as reported) | Shares | % Held | Reported Value (USD) | % Change |
|---|----------------------|--------|--------|----------------------|----------|
| 1 | Blackrock Inc. | 1,941,918,386 | 0.0806 (8.06%) | 327,970,595,026 | +0.0085 |
| 2 | Vanguard Capital Management LLC | 1,540,816,358 | 0.0639 (6.39%) | 260,228,473,762 | +0.0015 |
| 3 | FMR, LLC | 1,026,051,548 | 0.042600002 (4.26%) | 173,289,845,315 | +0.0324 |

Context: 7,753 institutions in total hold 71.384% of shares outstanding (0.74364 of float).

## 3. Paper Facts — "Attention Is All You Need" (arXiv:1706.03762)

- **Headline MT results (from abstract):** 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over existing best results (including ensembles) by over 2 BLEU. On WMT 2014 English-to-French, a new single-model state-of-the-art BLEU score of 41.8 was established after training for 3.5 days on eight GPUs — a small fraction of the training costs of the best models in the literature.
- **Base model stack:** Encoder — stack of N=6 identical layers (multi-head self-attention + position-wise fully connected feed-forward; residual connection + layer normalization around each sub-layer; d_model=512). Decoder — also a stack of N=6 identical layers, with a third sub-layer performing multi-head attention over the encoder output, plus masked self-attention to preserve the auto-regressive property.
- **Scaled dot-product attention:** $\mathrm{Attention}(Q, K, V) = \mathrm{softmax}(QK^T / \sqrt{d_k})V$. The dot products of the query with all keys are divided by $\sqrt{d_k}$ before the softmax; the scaling counteracts large dot-product magnitudes (variance $d_k$ for unit-variance components) that push softmax into regions with extremely small gradients.
- **Multi-head attention:** Queries, keys and values are linearly projected $h$ times with different learned linear projections to $d_k$, $d_k$ and $d_v$ dimensions; attention runs in parallel on each projected version; outputs are concatenated and projected again. The base model uses $h=8$ parallel attention heads, with $d_k = d_v = d_{model}/h = 64$.
- **How attention is used:** Multi-head attention is applied in three ways — encoder-decoder attention (queries from previous decoder layer, keys/values from encoder output), encoder self-attention, and decoder self-attention (masked).

## 4. Sources

- Company profile, market data and institutional ownership: Yahoo Finance (ticker NVDA), retrieved via the market data service on 2026-12-04.
- Paper: Vaswani et al., "Attention Is All You Need," arXiv:1706.03762 (https://arxiv.org/abs/1706.03762).

## 5. Knowledge base records

The verified facts above are now stored in the team knowledge graph (memory). Entities and relations created:

**Entities (6):**

| Entity | Type | Key observations |
|---|---|---|
| NVIDIA | company | NVDA, Technology / Semiconductors; market cap 4078186790912; institutions held 0.71384 (71.384%), insiders 0.04006; 7,753 institutions |
| Attention Is All You Need | paper | arXiv:1706.03762; 28.4 BLEU WMT 2014 En→De; 41.8 BLEU WMT 2014 En→Fr; scaled dot-product attention formulation |
| Transformer | architecture | N=6 encoder + N=6 decoder layers; h=8 parallel attention heads (d_k=d_v=64) |
| Blackrock Inc. | institutional holder | 1941918386 shares (top institutional holder of NVIDIA) |
| Vanguard Capital Management LLC | institutional holder | 1540816358 shares (top institutional holder of NVIDIA) |
| FMR, LLC | institutional holder | 1026051548 shares (top institutional holder of NVIDIA) |

**Relations (5):**

| From | Relation | To |
|---|---|---|
| Blackrock Inc. | is a top institutional holder of | NVIDIA |
| Vanguard Capital Management LLC | is a top institutional holder of | NVIDIA |
| FMR, LLC | is a top institutional holder of | NVIDIA |
| Attention Is All You Need | introduces | Transformer |
| Transformer | underpins | NVIDIA data-center AI business |
