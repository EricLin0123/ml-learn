# ML Learning Notebook Creator

Create a new educational Jupyter notebook on the topic: $ARGUMENTS, you should only work on this file as there may be other notebooks in progress. Keep in mind that I am preparing for a quantitative trading interview, so please explain the concepts as clearly as possible, even better, remind me whenever you think a certain concept is frequently tested in quant interviews.

## Goal

Keep in mind that I am preparing for a quantitative trading interview, so please explain the concepts as clearly as possible, even better, remind me whenever you think a certain concept is frequently tested in quant interviews.

Build a self-contained, beginner-friendly notebook that teaches `$ARGUMENTS` from first principles using math, code, and visualizations. The structure and content must be driven by what makes sense for the topic — not forced into a fixed template. When explaining mathematical concepts, use the same tone and style as Youtuber Statquest or 3Blue1Brown.

Also, when writing math equations, please add intuitive explanations or analogies to help the reader better understand what each term represents and how it contributes to the overall concept

---

## Non-negotiable style rules

### Formatting

- Section headers: `## 1 · Name`, `## 2 · Name`, ...
- End with a `| Concept | Key Idea |` summary table
- Use `---` separators between major sections in markdown cells

### Math

- Display equations: `$$...$$`
- Inline math: `$...$`
- Derive key formulas step-by-step; never drop steps without explanation
- Show gradient/derivative derivations explicitly when optimization is involved
- Standard notation: `\mathcal{L}` for loss, `\hat{y}` for predictions, `\mathbf{w}` for weight vectors
- Use blockquotes for key insights: `> **Key insight:** ...`

### Code

- Implement the core algorithm from scratch with numpy
- Split logically: one cell per concern (define → dataset → train → evaluate → plot)
- Training loops must record a `loss_history` list
- Print learned parameters and key metrics after training
- The libraries you have access to are:
  "jupyter",
  "matplotlib",
  "nbformat",
  "numpy",
  "scikit-learn",

### Plots

- Every major concept gets its own figure
- Color palette: `steelblue`, `tomato`, `mediumseagreen`, `darkorange`, `navy`
- Always set: `xlabel`, `ylabel`, `title`, `legend`, `ax.grid(alpha=0.3)`, `plt.tight_layout()`
- `plt.rcParams` block in the imports cell:
    ```python
    plt.rcParams.update({
        "figure.facecolor": "white",
        "axes.facecolor":   "#f8f8f8",
        "axes.grid":        True,
        "grid.color":       "white",
        "grid.linewidth":   1.2,
        "axes.spines.top":  False,
        "axes.spines.right": False,
        "font.family":      "sans-serif",
    })
    ```
- Add an `ipywidgets` interactive section when sliders meaningfully illustrate a hyperparameter (e.g. learning rate, k, regularization strength) — skip it when it adds no insight

### Tone

- Write for someone who knows Python and basic calculus but is new to ML
- Explain WHY before HOW in every section
- Define all jargon before using it
- Use `| Symbol | Meaning |` tables when introducing notation-heavy algorithms

---

## Content planning (do this first)

Before writing any cells, think through:

1. **What is the core mathematical idea?** (the function, distribution, or objective being learned)
2. **What kind of data does this algorithm naturally work with?** Choose a dataset that fits — it could be 1D, 2D, tabular, image patches, sequences, etc. Pick the simplest shape that makes the algorithm visible.
3. **What are the 2–3 plots that would give the most intuition?** Design those first, then write the sections that lead to them.
4. **What hyperparameters most affect behavior?** Consider a slider or side-by-side comparison for the most impactful one.
5. **What sections are needed?** Choose from below and add any topic-specific ones:

### Menu of sections (pick what fits, add what's missing)

| Section                                                      | Include when                                              |
| ------------------------------------------------------------ | --------------------------------------------------------- |
| Core mathematical object (function, distribution, kernel, …) | Always                                                    |
| Model formulation                                            | Always                                                    |
| Dataset                                                      | Always — synthetic is fine; shape must suit the algorithm |
| Loss function + why it's used                                | Always when there's an optimization step                  |
| Loss landscape visualization                                 | When the loss is 1D or 2D visualizable                    |
| Optimization algorithm (from scratch)                        | Always when gradient descent or similar is used           |
| Training loop + loss curve                                   | Always when iterative training occurs                     |
| Fitted model over data                                       | Always                                                    |
| Evaluation metric                                            | Always                                                    |
| Effect of a key hyperparameter                               | When it meaningfully changes behavior                     |
| Interactive widget                                           | When sliders give clear intuition                         |
| Summary table                                                | Always (last cell)                                        |

---

## Execution steps

1. Plan the sections for `$ARGUMENTS` using the menu above
2. Write all cells using `NotebookEdit` (preferred) or a full `.ipynb` JSON with `Write`
3. Filename: snake_case of the topic, e.g. `k_means.ipynb`, `naive_bayes.ipynb`
4. Save to `/Users/wanchuan/ml-learn/`
5. Confirm the file is created and list the section titles chosen
