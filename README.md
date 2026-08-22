# Shakespeare-ChatGPT

A simple, readable implementation of GPT — trainable on a single GPU or even a CPU. This repo lets you train a small character-level language model on Shakespeare's text and watch it learn to generate Shakespeare-style writing.

Based on Andrej Karpathy's [nanoGPT](https://github.com/karpathy/nanoGPT) and his ["Let's build GPT" video](https://www.youtube.com/watch?v=kCc8FmEb1nY).

## What's in here

| File | Purpose |
|---|---|
| `model.py` | The GPT architecture — attention, transformer blocks, the full model |
| `train.py` | Training loop |
| `sample.py` | Generate text from a trained model |
| `data/shakespeare_char/prepare.py` | Downloads and prepares the Shakespeare dataset |
| `config/train_shakespeare_char.py` | Hyperparameters for the small "baby GPT" |

## Setup

```bash
# 1. Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux

# 2. Install dependencies
pip install torch numpy transformers datasets tiktoken wandb tqdm
```

## Quick start

```bash
# 1. Prepare the dataset (downloads Shakespeare text, converts to integers)
python data/shakespeare_char/prepare.py

# 2. Train the model
python train.py config/train_shakespeare_char.py

# If you don't have a GPU, add these flags to speed things up:
python train.py config/train_shakespeare_char.py --device=cpu --compile=False --max_iters=2000 --eval_iters=100

# 3. Generate text from your trained model
python sample.py --out_dir=out-shakespeare-char
```

That's it — training takes a few minutes on a GPU, longer on CPU. Once it finishes, `sample.py` will print out generated text in a Shakespeare-ish style.

## Notes

- Model checkpoints are saved to `out-shakespeare-char/` — not included in this repo (regenerate them by training).
- `venv/`, `__pycache__/`, and generated data files (`.bin`, `.pkl`) are excluded.
