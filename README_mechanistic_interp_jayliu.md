# 🧠 Mechanistic Interpretability — Explaining a Tiny Brain  
**Author:** Jay Liu (Duke MIDS)  
**Course:** AIPI-590 — Explainable AI  
**Date:** November 2025  

---

## 🌱 Overview
This mini project explores **mechanistic interpretability**—understanding what’s going on inside a neural network—through a tiny, self-contained example.  
I trained a **small MLP** on a **3-bit parity task** and then investigated what each neuron seems to be doing.  

The story is part detective work, part narrative: what patterns appear inside the network, and how can we interpret them in human terms?

---

## ⚙️ Setup & Task

- **Task:** Predict whether a 3-bit binary vector has an **odd** or **even** number of ones (the parity function).  
- **Model:** Tiny MLP with one hidden layer of 4 neurons (`tanh` activation).  
- **Why parity?** It’s simple yet nonlinear—perfect for testing whether small neural units learn compositional features.

Training takes **under 10 seconds** on CPU and achieves **100% accuracy** on all 8 input patterns.

---

## 🔍 Exploration and Findings

### Step 1. Peeking Inside  
I visualized:
- **Weight matrices** to see sign patterns.  
- **Hidden activations** for each input combination.  
- **Neuron–label correlations** to find which neurons track the target parity.  

### Step 2. Causal Tests  
Using **single-neuron ablation**, I set each hidden activation to zero and re-evaluated accuracy.  
One neuron (n₀) stood out: when ablated, performance dropped from 100% → 50%.  

### Step 3. Saliency Analysis  
I computed the **input gradient of that neuron’s activation**.  
The saliency was spread fairly evenly across all three input bits—matching intuition that parity is a global feature, not a single-bit cue.

---

## 🧩 Mechanistic Hypothesis
> “One hidden neuron acts as an **odd-parity detector** — flipping its sign in response to whether the number of ones is odd or even.”

### Evidence
- Highest correlation with label (`r ≈ 0.48`).  
- Structured activation heatmap (clear sign change across even vs. odd).  
- Large drop in accuracy when ablated.  
- Broad input saliency pattern consistent with global logic.

### Interpretation
The neuron builds an approximate **XOR-like** decision boundary by summing inputs with alternating positive/negative weights and pushing them through a `tanh`.  
The final linear layer recombines these features to output parity perfectly.

---

## 💭 Reflection

**What I learned:**  
Even a “black box” as small as four neurons shows *structured, interpretable behavior*. By visualizing and perturbing, the abstract math becomes tangible.

**Surprising parts:**  
Multiple neurons contributed meaningfully—removing just one damaged performance but didn’t completely destroy it.  
Activations were often near ±1, suggesting crisp separations through the binary cube.

**If I had more time:**  
I’d visualize *training evolution*—how correlations grow over epochs—and explore a 4-bit parity extension to see feature reuse and redundancy.

---

## 📊 Visuals Included
1. **Loss curve** over 2000 epochs  
2. **Hidden activation heatmap** (inputs × neurons)  
3. **Ablation bar chart** (accuracy drop per neuron)  
4. **Input saliency bar chart** for top neuron  

---

## ✅ Submission Checklist

- [x] Custom model and task  
- [x] Internal inspection (weights, activations, ablation, saliency)  
- [x] Mechanistic hypothesis with evidence  
- [x] Reflection and interpretation  
- [x] Google Colab + GitHub integration  

**GitHub Repo:** [*add your repo link here*]  
**Colab Notebook:** [*add your Colab share link here*]

---

## 🧠 TL;DR Blog Summary
> “A 4-neuron MLP learned to compute parity — a nonlinear logic task — by evolving a neuron that behaves like a global parity switch. Mechanistic interpretability turns a math problem into a detective story: one neuron’s sign tells us whether the world has an odd number of ones.”
