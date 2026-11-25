# Perplexity Explorer

An interactive web application demonstrating language model probabilities, step-by-step perplexity calculation, and next-token predictions in real time.

🔗 **Live Vercel Demo:** [https://perplexity-explorer-hazel.vercel.app](https://perplexity-explorer-hazel.vercel.app)  
🌐 **GitHub Pages Demo:** [https://ayush-aiwbk.github.io/perplexity-explorer/](https://ayush-aiwbk.github.io/perplexity-explorer/)

Built as a single-file application with clean HTML, CSS, and plain JavaScript—no frameworks, no backend, and no API keys required. It runs the `Xenova/distilgpt2` language model directly in your browser using **Transformers.js**.

## Features

- **Section 1 – Type a Sentence**:
  - Input any custom sentence or pick from one of the quick samples (`"I love Python"`, `"Python love I"`, `"The capital of France is Paris"`).
  - Runs in-browser causal language model inference (`Xenova/distilgpt2` with 8-bit quantization) via `@huggingface/transformers`.
  - Computes stable softmax probabilities for every token with start marker context.

- **Section 2 – Probability of Each Token → Perplexity**:
  - Detailed token breakdown table displaying `#`, `Token` (spaces shown as `␣`), `Probability P`, and `1/P`.
  - **Step 1**: Multiplies all $1/P$ values.
  - **Step 2**: Identifies sequence length $N$.
  - **Step 3**: Computes Perplexity $= (\text{Product})^{1/N}$ using logarithms ($\exp(\text{mean}(-\ln P))$) to avoid numerical overflow.

- **Section 3 – What Does the Model Predict Next?**:
  - Examines logits at the final position.
  - Visualizes top 8 next-token predictions with horizontal percentage bars, highlighting the top candidate.

- **Section 4 – Try It by Hand (Simulated, not from the model)**:
  - Interactive playground to add/remove custom tokens and probabilities.
  - Built-in presets:
    - `"I love Python"` ($P = [0.5, 0.8, 0.2] \implies \text{Perplexity } 2.32$)
    - `"All 1/8"` ($8 \text{ tokens at } 0.125 \implies \text{Perplexity } 8.00$)
    - `"One surprising word"` ($P = [0.9, 0.9, 0.9, 0.01] \implies \text{Perplexity } 3.42$)
  - Live table and 3-step calculation updates as you type.

## Running Locally

Clone the repository and serve `index.html` using any static file server:

```bash
git clone https://github.com/Ayush-aiwbk/perplexity-explorer.git
cd perplexity-explorer
python3 -m http.server 8080
```

Open `http://localhost:8080` in any modern web browser.
