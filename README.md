# olmo3-code-300m-bitnet

Pre-training a **~300M parameter** code-specialized language model from scratch using a **BitNet b1.58** variant of the [OLMo 3](https://allenai.org/olmo) architecture on PHP/JS/Python/C source code from the [Training-Datasmith](https://github.com/Training-Datasmith) organization.

## Architecture

| Parameter | Value |
|-----------|-------|
| Hidden dim | 1024 |
| Layers | 16 |
| Attention heads | 16 (GQA: 4 KV heads) |
| FFN dim | 3072 (SwiGLU) |
| Context length | 1024 tokens |
| Vocab size | 100,352 (OLMo-2 tokenizer) |
| Total params | ~295.9M |

Key features: BitLinear (ternary {-1, 0, 1} weights, int8 activations), RoPE positional encoding, Group Query Attention, SwiGLU FFN, Pre-norm transformer with Straight-Through Estimation.

## Training

- **Environment:** Kaggle T4 x2 (2× 16 GB VRAM)
- **Dataset:** 27 curated PHP repos (ecommerce carts + frameworks) from Training-Datasmith org
- **Steps:** 20,000 with cosine LR schedule (3e-4 peak, 500 warmup)
- **Batch:** 2 × 8 gradient accumulation = effective 16

## Dependencies

Uses the [kaggle-utilities](https://github.com/Training-Datasmith/kaggle-utilities) package for model architecture, data pipeline, and training loop.

## License

GPL-3.0
