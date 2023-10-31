# Latex functionality

Lambda feedback uses one content source to serve two outputs: _web_ and _PDF_. Each output has different requirements, and content must meet both requirements in order to serve both outputs.

## Content formatting

All content is formatted in [_markdown_](https://www.markdownguide.org/basic-syntax/). Headings, font style, lists, tables, images, $\LaTeX$, can all be created using standard markdown.

Special attention is required when formatting $\LaTeX$ which, although it is formatted using standard markdown (i.e. delimited by the `$` for 'inline formulas', and `$$` for an equation environment), must use a subset of $\LaTeX$ in order to compile for both outputs. This sometimes requires a compromise by the author.

## The milkdown editor

All content in Lambda Feedback is stored as markdown (ASCII content), however it is always input/edited using the [milkdown](https://milkdown.dev/online-demo) editor. This editor has the advantage of providing live interactive previews of content, including $\LaTeX$ via katex.

## Web requirements: katex

$\LaTeX$ content is rendered in the web browser using the [katex](https://www.katex.org/) Javascript library. The [katex home page](https://www.katex.org/) has an intereactive input where content is rendered and can be checked for validity. The [documentation](https://katex.org/docs/supported) lists which functions are supported.

Katex is a **subset of** $\LaTeX$. Therefore some functions that work in $\LaTeX$ do not work in katex and won't render on the web. For example, the `tikz` package - which is a complex graphics package - is not supported by katex. Unsupported packages have knock-on effects, for example while the `\cancel{}` function is supported, `\cancelto{}{}` is not because it relies on `tikz`.

Ensuring that content renders correctly on the web is straightforward because the editor gives a live preview - and will indicate when errors occur.

## PDF requirements: pandoc and PDFlatex/XeTeX

When a Problem Set is _saved_ in the editor, the PDF is automatically compiled by sending the markdown content to [Pandoc](https://pandoc.org/), which internally uses $\LaTeX$ (either PDFlatex of xelatex - depending on the settings within the Lambda Feedback stack) to render a PDF.

Problems can occur with PDF compilation even if the web rendering is successful, because it uses different libraries to the web browser. If the PDF fails to compile, a red error bar will appear and provide the location of the error within the Problem Set (identifying which question), and the error that Pandoc returned.

One key limitation of the Lambda Feedback system is that it uses markdown content, so cannot produce all the richness of a full $\LaTeX$ document (and the AMS math library). All equation environments in markdown are signalled by the `$$` delimiter which is equivalent to `\begin{equation*}`. This rules out using alternative _primary environments_, such as `align`, `gather`, `multiline`, `alignat`, `falign`.

You can use _subordinate environments_ within an equation environment, for example the following is valid:

```
$$
\begin{aligned}
a & b\\
c & d
\end{aligned}
$$
```

Here the suffix `-ed` in `aligned` implies a subordinate environment; likewise `gathered`, `alignedat` etc. are all valid within an equation environment.

#### Warning: No blank lines allowed in `aligned` subordinate environment

If a blank line is present within a subordinate environment `\begin{aligned}` then Pandoc will fail to compile the PDF. For example:

```Faulty code example:
$$
\begin{aligned}
a & b\\
c & d

\end{aligned}
$$
```

The above will fail to compile the PDF. But removing the blank line will solve the problem.

For further reading search for the AMS math package and related literature.

## Numbering equations

Equation numbering is problematic and our advice is to use manual numbering. Automatic numbering is possible, for example using `\begin{equation}` within a `$$` environment. Note that sometimes the equation numbers continue counting from one environment to the next, while at other times they don't. You cannot use `\ref` to refer to automatic equation numbers.

An alternative approach is to use an unnumbered aligned environment, and to add an extra column with the equation number in (e.g. `&(2)`).

For some _ad hoc_ good practice tips, see [good practice](../guides/good-practice.md).
