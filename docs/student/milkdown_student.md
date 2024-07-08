# Text Editing

The [Milkdown editor](https://milkdown.dev/online-demo) is widely used in Lambda Feedback wherever rich text input is required.
On the student interface, it is used to add personal solution notes, and to write comments.

It accepts:

- Standard [Markdown](https://www.markdownguide.org/basic-syntax/)
- [$\LaTeX$](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- Images (paste or drag and drop)
- Videos (paste a URL)

## $\LaTeX$
LaTeX is a typesetting system widely used in academia to produce well-formatted documents. It is mostly used in Lambda Feedback for its
capability to render complex mathematical expressions clearly and accurately. 
  
As an example, the following LaTeX code: 
```
\int_V \nabla \cdot \vec{f} \mathrm{d}V = \oint_S \vec{f} \cdot \hat{n} \mathrm{d}S
```
Produces the following output:

\[ \int_V \nabla \cdot \vec{f} \mathrm{d}V = \oint_S \vec{f} \cdot \hat{n} \mathrm{d}S \]

In the Milkdown editor, anything surrounded by dollar signs (like `$ x^2 $`) will be interpreted as LaTeX. 
Only the subset supported by [KaTeX](https://katex.org/docs/supported), which includes most common LaTeX functions, can be used.
