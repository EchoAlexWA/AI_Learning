# Single head attention
Assume $X \in \mathbb{R}^{n \times d}$ is the input matrix, where $n$ is the sequence length and $d$ is the feature dimension.
We define three learnable weight matrices:
- Query weight matrix: $W_Q \in \mathbb{R}^{d \times d_k}$
- Key weight matrix: $W_K \in \mathbb{R}^{d \times d_k}$
- Value weight matrix: $W_V \in \mathbb{R}^{d \times d_v}$
- Output weight matrix: $W_O \in \mathbb{R}^{d_v \times d}$
- Here, $d_k$ and $d_v$ are the dimensions of the query/key and value vectors, respectively.
The attention mechanism can be computed as follows:
1. Compute the query, key, and value matrices:
   $$
   Q = X W_Q \in \mathbb{R}^{n \times d_k} \\
   K = X W_K \in \mathbb{R}^{n \times d_k} \\
   V = X W_V \in \mathbb{R}^{n \times d_v}
   $$

2. Compute the attention scores:
    $$
    \text{Scores} = \frac{Q K^T}{\sqrt{d_k}} \in \mathbb{R}^{n \times n}
    $$

3. Apply the softmax function to obtain the attention weights:
    $$
   \text{AttentionWeights}= A = \text{softmax}(\text{Scores}) \in \mathbb{R}^{n \times n}
    $$
    where the softmax function is applied row-wise. (e.g. for each row $i$:
    $\text{AttentionWeights}_{i,j} = \frac{e^{\text{Scores}_{i,j}}}{\sum_{k=1}^{n} e^{\text{Scores}_{i,k}}}$).

4. Compute the weighted sum of the value vectors:
    $$
   \text{Context Vector}= Z = AV \in \mathbb{R}^{n \times d_v}
    $$

The output of the attention mechanism is the context vector $Z$.

# Multi-head attention
Multi-head attention extends the single head attention mechanism by allowing the model to jointly attend to information from different representation subspaces at different positions. Instead of having a single set of query, key, and value weight matrices, we have multiple sets for each head.
Assume we have $h$ heads. $X\in \mathbb{R}^{n \times d}$. For each head $i$ (where $i = 1, 2, \ldots, h$), we define separate weight matrices:
- Query weight matrix: $W_Q^{(i)} \in \mathbb{R}^{d \times d_k}$
- Key weight matrix: $W_K^{(i)} \in \mathbb{R}^{d \times d_k}$
- Value weight matrix: $W_V^{(i)} \in \mathbb{R}^{d \times d_v}$
- $d_v * h = d$
The multi-head attention mechanism can be computed as follows:
1. For each head $i$, compute the query, key, and value matrices:
   $$
   Q^{(i)} = X W_Q^{(i)} \in \mathbb{R}^{n \times d_k} \\
   K^{(i)} = X W_K^{(i)} \in \mathbb{R}^{n \times d_k} \\
   V^{(i)} = X W_V^{(i)} \in \mathbb{R}^{n \times d_v}
   $$
2. For each head $i$, compute the attention scores:
    $$
    \text{Scores}^{(i)} = \frac{Q^{(i)} (K^{(i)})^T}{\sqrt{d_k}} \in \mathbb{R}^{n \times n}
    $$
3. For each head $i$, apply the softmax function to obtain the attention weights:
    $$
    \text{AttentionWeights}^{(i)} = A^{(i)} = \text{softmax}(\text{Scores}^{(i)}) \in \mathbb{R}^{n \times n}
    $$
4. For each head $i$, compute the weighted sum of the value vectors:
    $$
    \text{Context Vector}^{(i)} = Z^{(i)} = A^{(i)} V^{(i)} \in \mathbb{R}^{n \times d_v}
    $$
5. Concatenate the context vectors from all heads:
    $$
    \text{Concatenated Context} = Z_{concat} = [Z^{(1)}; Z^{(2)}; \ldots; Z^{(h)}] \in \mathbb{R}^{n \times (h \cdot d_v)}
    $$

The final output is in $\mathbb{R}^{n \times d}$.

