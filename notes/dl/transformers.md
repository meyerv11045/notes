# Transformers

## Attention

- token -> query vector $q \in \mathbb{R}^{d_{attn}}$
- context tokens -> key vectors $k_t \in \mathbb{R}^{d_{attn}}$ and value vectors $v_t \in \mathbb{R}^{d_{val}}$
- $q^Tk_t$ represents how important token $t$ is for predicting the current token $q$

### Types

- Bidirectional (aka unmasked)- applies attention to each token with all the tokens as the context
- Unidirectional (aka masked)- applies attention to each token with the preceding tokens + itself as the context
    - can think of the following tokens as being masked
- Cross- given two token sequence representations $X,Z$ (can be diff lengths), applies attention to each token of the primary sequence $X$ with the second sequence $Z$ as the context
- Dense- uses all of the context
- Sparse- uses a subset of the context