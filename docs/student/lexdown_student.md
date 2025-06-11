# Text Editing

The lexdown is widely used in Lambda Feedback wherever rich text input is required.
On the student interface, it is used to add personal solution notes, and to write comments.

It accepts:

- Standard [Markdown](https://www.markdownguide.org/basic-syntax/)
- [$\LaTeX$](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- Images (paste or drag and drop)
- Videos (paste a URL)

## LaTeX
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

### LaTeX equations in 5 minutes
#### Numbers and letters
Numbers and Latin letters can be entered as you would expect:
```
1, 2, 3, 3.14159, -2.5, x, y, z
```

\[ 1, 2, 3, 3.14159, -2.5, x, y, z \]

Subscripts can be written with `_` and superscripts can be written with `^`, for example in `x^2` ($x^2$) or `x_2` ($x_2$).
Only the first character or command after a `_` or `^` will be taken. To subscript or superscript multiple characters, they can be 
grouped in curly braces, like this: `V_{ab}` ($V_{ab}$).

#### Basic functions
Functions in LaTeX start with a backslash `\`.

Some common functions include Greek letters:

- `\pi` ($\pi$)
- `\delta` ($\delta$)
- `\Delta` ($\Delta$) 
- etc.

Equalities: 

- `\approx` ($\approx$)
- `\ne` ($\ne$)
- `\gt` ($\gt$)
- etc.

Symbols/operators:
- `\int` ($\int$)
- `\sum` ($\sum$)
- `\sin` ($\sin$)
- `\ln` ($\ln$)
- etc.

#### Functions with arguments
Some functions take arguments. Arguments are given between curly braces `{}`. 

Some commonly functions with arguments are:

- `\sqrt{x}` ($\sqrt{x}$). This places a square root sign around the argument.
- `\frac{x}{y}` ($\frac{x}{y}$). This command takes two arguments, and produces a fraction with the first argument in the numerator and the second on the denominator.

- Diacritics:

    - `\vec{x}` ($\vec{x}$).
    - `\dot{x}` ($\dot{x}$). 
    - `\hat{x}` ($\hat{x}$).
    - etc.

- `\mathrm{x}` ($\mathrm{x}$). This formats the argument as regular, upright text, rather than italics. Should be used for units and operators (e.g. $\frac{\mathrm{d}y}{\mathrm{d}x}$).

#### Nesting
Functions can be nested arbitrarily. For example, a square root may contain a fraction, which may contain another square root:
```
\sqrt{ \frac{-b \pm \sqrt{b^2 - 4ac }}{2a} }
```

\[\sqrt{ \frac{-b \pm \sqrt{b^2 - 4ac }}{2a} }\]

#### Going further
If you are unsure of the correct function to use to produce the desired result, there is a list of all supported KaTeX functions [here](https://katex.org/docs/supported.html).
