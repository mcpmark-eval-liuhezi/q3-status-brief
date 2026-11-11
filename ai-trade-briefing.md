# The Paper That Started the AI Trade

**Working title:** The Paper That Started the AI Trade
**Status:** Draft for research meeting circulation
**Verification status:** Company facts and paper facts verified against primary sources (Yahoo Finance market data service and the arXiv paper source, arXiv 1706.03762) prior to publication.

---

## 1. Company Snapshot: NVIDIA Corporation (NVDA)

**Market data (as returned by the data service, unrounded):**

| Field | Value |
|---|---|
| Ticker | NVDA (NasdaqGS) |
| Sector | Technology |
| Industry | Semiconductors |
| Market cap | 4078186790912 USD (~4.08 trillion) |
| Shares outstanding | 24147000000 |
| Institutional ownership | heldPercentInstitutions 0.71384 (71.384%) |
| Insider ownership | heldPercentInsiders 0.04006 (4.006%) |
| Current price | 168.89 USD (previous close 178.67; day range 165.89 - 174.65) |
| Trailing P/E | 21.351454 |
| Forward P/E | 10.6033 |
| Dividend yield | 0.59% |
| Beta | 2.247 |
| Analyst consensus | strong_buy (recommendationMean 1.32258, 57 analyst opinions, mean target 325.7772) |
| Revenue (TTM) | 302970011648 USD |
| Net income to common | 192880001024 USD |
| Full-time employees | 42000 |
| Headquarters | Santa Clara, CA, United States |

**Business description (per data service):** NVIDIA Corporation operates as a data center scale AI infrastructure company in the United States, Taiwan, China, Hong Kong, Europe, and internationally. It operates through Compute & Networking and Graphics segments. The Compute & Networking segment provides data center accelerated computing and networking platforms and artificial intelligence solutions and software, and automotive platforms and autonomous and electric vehicle solutions. The Graphics segment offers GeForce GPUs for gaming and PCs; Quadro/NVIDIA RTX GPUs for enterprise workstation graphics.

**Officers of note:** Jen-Hsun "Jensen" Huang (Co-Founder, CEO & Director), Colette M. Kress (Executive VP & CFO), William J. Dally (Chief Scientist & Senior VP of Research), Chris A. Malachowsky (Co-Founder), Scott C. Gawel (Chief Accounting Officer).

---

## 2. Institutional Ownership Table

Institutional ownership of NVIDIA is 0.71384 (71.384%) of shares out. The three largest institutional holders by most recently reported share count, as reported by the data service:

| # | Holder | Shares Held | % of Company | Reported Value (USD) | % Change |
|---|---|---|---|---|---|
| 1 | Blackrock Inc. | 1941918386 | 0.0806 (8.06%) | 327970595026 | 0.0085 |
| 2 | Vanguard Capital Management LLC | 1540816358 | 0.0639 (6.39%) | 260228473762 | 0.0015 |
| 3 | FMR, LLC | 1026051548 | 0.042600002 (4.26%) | 173289845315 | 0.0324 |

All three top holders report the same Date Reported (epoch 1782777600000). Together they represent the largest institutional concentration in the company. (Next largest: State Street Corporation with 1009783437 shares at 0.0419.)

---

## 3. Paper Facts: "Attention Is All You Need" (arXiv 1706.03762)

**Headline machine translation results (from the abstract):**

- **28.4 BLEU on the WMT 2014 English-to-German translation task**, improving over the existing best results, including ensembles, by over 2 BLEU.
- **41.8 BLEU on the WMT 2014 English-to-French translation task** — a new single-model state-of-the-art BLEU score, achieved after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature.
- The abstract also notes the Transformer generalizes well to other tasks, applied successfully to English constituency parsing with both large and limited training data.

**Base model stack:**

- **Encoder:** a stack of **N=6 identical layers**, each with two sub-layers — a multi-head self-attention mechanism and a simple, position-wise fully connected feed-forward network. Each sub-layer is wrapped in a residual connection followed by layer normalization: LayerNorm(x + Sublayer(x)). All sub-layers and embedding layers produce outputs of dimension d_model = 512.
- **Decoder:** also a stack of **N=6 identical layers**, adding a third sub-layer that performs multi-head attention over the output of the encoder stack; decoder self-attention is masked to prevent positions from attending to subsequent positions, preserving the auto-regressive property.

**Attention mechanism (as described in the paper):**

- **Scaled Dot-Product Attention:** queries and keys have dimension d_k, values have dimension d_v. The dot products of the query with all keys are computed, divided by sqrt(d_k), and a softmax is applied to obtain the weights on the values. In matrix form:

  Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V

- **Why the scaling:** for large d_k, the dot products grow large in magnitude, pushing the softmax into regions where it has extremely small gradients. To counteract this effect, the dot products are scaled by 1/sqrt(d_k). (For small d_k the two mechanisms perform similarly; dot-product attention without scaling is much faster and more space-efficient in practice since it uses optimized matrix multiplication code.)
- **Multi-Head Attention:** instead of a single attention function with d_model-dimensional keys, values and queries, the queries, keys and values are linearly projected h times with different, learned linear projections to d_k, d_k and d_v dimensions respectively. The attention function is performed in parallel on each projected version, yielding d_v-dimensional outputs that are concatenated and projected again:

  MultiHead(Q, K, V) = Concat(head_1, ..., head_h)W^O, where head_i = Attention(QW^Q_i, KW^K_i, VW^V_i)

- **Number of parallel heads in the base model: h = 8.** For each head, d_k = d_v = d_model/h = 64. Due to the reduced dimension of each head, the total computational cost is similar to that of single-head attention with full dimensionality. Multi-head attention allows the model to jointly attend to information from different representation subspaces at different positions.
- Multi-head attention is used in three ways in the model: encoder-decoder attention layers, encoder self-attention layers, and (masked) decoder self-attention layers.

---

## 4. Sources

- ** paper:** "Attention Is All You Need", arXiv:1706.03762 (Vaswani et al.) — abstract and Model Architecture section verified against the paper source.
- ** Company data:** NVDA market data and institutional holder data via the Yahoo Finance market data service (stock info, major holders, institutional holders).
- ** Gist:** this file, `ai-trade-briefing.md`, published for research meeting circulation.

---

## 5. Knowledge base records

The following entities and relations were created in our team knowledge graph (read back and verified after creation):

**Entities (6):**

1. **NVIDIA** (Company) — NVDA, NasdaqGS; sector Technology / industry Semiconductors; market cap 4078186790912 USD; heldPercentInstitutions 0.71384; 42000 full-time employees; headquarters Santa Clara, CA; current price 168.89 USD; trailing P/E 21.351454; forward P/E 10.6033; dividend yield 0.59%; beta 2.247; analyst consensus strong_buy (57 opinions, mean target 325.7772); revenue TTM 302970011648 USD; net income to common 192880001024 USD; organizes through Compute & Networking and Graphics segments; CEO Jen-Hsun "Jensen" Huang.
2. **Attention Is All You Need** (Research Paper) — arXiv 1706.03762; 28.4 BLEU WMT 2014 English-to-German (over 2 BLEU better than prior best including ensembles); 41.8 BLEU WMT 2014 English-to-French (new single-model SOTA, 3.5 days on 8 GPUs); N=6 encoder layers and N=6 decoder layers; d_model=512; Scaled Dot-Product Attention with 1/sqrt(d_k) scaling; h=8 parallel attention heads, d_k=d_v=64.
3. **Transformer** (Architecture) — introduced by arXiv 1706.03762; encoder-decoder structure; N=6 identical layers in both encoder and decoder stacks (decoder has a third sub-layer for encoder-decoder attention); d_model=512, d_ff=2048; scaled dot-product attention formula Attention(Q,K,V)=softmax(QK^T/sqrt(d_k))V; 8 parallel heads with d_k=d_v=64; no recurrence/convolutions; sinusoidal positional encodings.
4. **Blackrock Inc.** (Institutional Holder) — top institutional holder of NVIDIA; 1941918386 shares; pctHeld 0.0806; value 327970595026 USD; pctChange 0.0085; Date Reported 1782777600000.
5. **Vanguard Capital Management LLC** (Institutional Holder) — top institutional holder of NVIDIA; 1540816358 shares; pctHeld 0.0639; value 260228473762 USD; pctChange 0.0015; Date Reported 1782777600000.
6. **FMR, LLC** (Institutional Holder) — top institutional holder of NVIDIA; 1026051548 shares; pctHeld 0.042600002; value 173289845315 USD; pctChange 0.0324; Date Reported 1782777600000.

**Relations (5):**

1. Blackrock Inc. —**is a top institutional holder of**→ NVIDIA
2. Vanguard Capital Management LLC —**is a top institutional holder of**→ NVIDIA
3. FMR, LLC —**is a top institutional holder of**→ NVIDIA
4. Attention Is All You Need —**introduces**→ Transformer
5. Transformer —**underpins**→ NVIDIA

*Knowledge graph read back post-creation and confirmed: 6 entities with the key facts as observations (holder share counts, paper BLEU results and layer counts, number of attention heads), and 5 relations with the exact labels specified above.*

---

*Prepared as a factual spine for the thematic briefing "The Paper That Started the AI Trade." All figures above are reported exactly as returned by the data services; no rounding or conversion has been applied.*
