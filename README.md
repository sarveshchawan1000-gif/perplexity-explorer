# Perplexity Explorer

An interactive, client-side web application for understanding language model perplexity, token probabilities, and next-token distributions using [Transformers.js](https://huggingface.co/docs/transformers.js) and GPT-2 (`Xenova/distilgpt2`).

## Features

- **Interactive Sentence Analysis**:
  - Tokenizes sentences and prepends GPT-2's start token (`<|endoftext|>`, ID `50256`).
  - Evaluates distilgpt2 locally in the browser with `q8` quantization.
  - Computes exact token probabilities using numerically stable softmax over preceding-position logits.
  - Includes sample presets: *"I love Python"*, *"Python love I"*, and *"The capital of France is Paris"*.

- **Token Probabilities & Perplexity Breakdown**:
  - Displays token sequences with whitespace rendered as `␣`.
  - Computes $P$ and $1/P$ for every token.
  - Shows intermediate calculation steps:
    1. Multiplication of all $1/P$ values (with scientific notation to avoid numeric overflow).
    2. Number of scored tokens $N$.
    3. Perplexity calculated in log-space: $\text{Perplexity} = \exp\left(\frac{1}{N}\sum -\ln(P)\right)$.

- **Next-Token Predictions**:
  - Extracts logits from the final sequence position to show the top 8 predicted next tokens.
  - Visualized with percentage bars and highlighting for the most likely continuation.

- **Try It by Hand (Simulated Playground)**:
  - Experiment with custom tokens and probabilities to observe how surprises compound into perplexity.
  - Live calculations on every keystroke.
  - Built-in presets:
    - *I love Python* ($0.5, 0.8, 0.2 \implies \approx 2.32$)
    - *All 1/8* ($8 \times 0.125 \implies 8.00$)
    - *One surprising word* ($0.9, 0.9, 0.9, 0.01 \implies \approx 3.42$)

## Quick Start

Open `index.html` in any modern web browser or serve locally:

```bash
# Using Python
python3 -m http.server 8000

# Using Node.js
npx serve .
```

Navigate to `http://localhost:8000`. No backend, build step, or API key required!
