# Good practice

## Formatting & style for readability

### Romanised text for operators and units

Use romanised operators and scientific units to distinguish them from variables, which are italicised.

*   **Operators:** Use `\sin`, `\cos`, `\log`, `\det`, etc. For derivatives, use `\mathrm{d}` as in `\dfrac{\mathrm{d}y}{\mathrm{d}x}`.
    *   **Correct:** $\sin(x)$, $\dfrac{\mathrm{d}}{\mathrm{d}x}$
    *   **Incorrect:** $sin(x)$, $\frac{d}{dx}$

*   **Units:** Use `\text{...}` or `\mathrm{...}` (mathrm allows for numbers in the units, i.e. $\mathrm{m^2}$). Ensure the unit's case is correct (e.g., `m` for milli, `M` for mega).
    *   **Correct:** $5 \text{ m}$, $10 \text{ kN}$
    *   **Incorrect:** $5 m$, $10 kN$

### Space between numbers and units

Put appropriate space between a number and its unit, such as `5 m` or `3 kg`, according to the SI conventions.

e.g. `$5 \text{ m}$` to get $5 \text{ m}$

### Empty lines

Using empty lines can improve the readability and neatness of your content.

Empty lines are often useful before and after an equation, and between paragraphs of text. An empty line in markdown requires _two spaces_ on the line, otherwise the line is ignored.

Alternatively, adding empty LaTeX text, `\text{}`, can work if all else fails.

## Using platform features effectively

### Save and publish as you go

Saving and publishing work regularly is recommended to prevent accidental data loss.

### Add tests to response areas

Tests allow you to enter potential student responses, define whether they are correct or not, then run the evaluation function on those student responses. This allows you to quickly test whether or not the evaluation function works as expected.

In a response area, press `Configure` then `Test`.

### Pre-response area text

Use pre-response area text to make clear what students should write.

Pre-response area text is found under `Configure` - `Input` in the evaluation function.

You can use LaTeX in the pre-response area text.

![Image showing a pre-response area](images/pre_response_area.png)

### Live preview

Live preview is on by default with the Expression response area. Live preview instantly renders a student's input. This is very useful for long/complicated equations, as it allows students to ensure their input is correct.

Live preview settings are found under `Configure` - `Input` - `Display settings`.

![Image showing a live-preview to a student's response](images/live_preview.png)

### Branching

Branching is a feature for `worked solutions`. It allows you to have different solution pathways

Usage examples:

- When a question can be solved via multiple different methods, branching can be used for each method.
- When a question has multiple parts, where each part involves substitution of different values, branching can be used for each part.

![gif showing the branching feature](images/branching.gif)

### Audio clips

Drag + drop an audio file into the editor, or record audio on the 'Insert v' drowpdown in Lexdown.

### Input symbols

Input symbols help in two ways:

1. Show the evaluation function how to interpret responses
2. (If displayed) show the student how to express their response

Input symbols require a display symbol where single dollars to delimit inline-math latex are recommended (e.g. `$x$` will display to students as $x$) and corresponding code to be used by the evaluation function (e.g. `x`). Displaying symbols to students is helpful when it's not clear how to type a symbol as code; for exaxmple symbol $\rho$ may be inserted is `rho` or `r` or `p` depending on the opinion of the teacher.

Providing alternatives is optional but recommended. Alternatives help provide higher reliability feedback. For example, alternatives to `rho` could be `Rho`, `RHO`, `r`, `R`, `p`, `P` - although some of these may not be acceptable if they have another meaning in the context in question. 



## Latex help

### Use `\dfrac` for bigger fractions

Use `$\dfrac{numerator}{denominator}$` for bigger fractions when you need to display them more clearly or emphasize them. For example, `$\dfrac{3}{4}$` will produce a bigger fraction than `$\frac{3}{4}$`:

$\dfrac{3}{4} \quad$    (dfrac)

$\frac{3}{4} \quad$    (frac)

Alternatively, you can use `$\displaystyle$` at the start of an inline equation to render everything afterwards full-size (as in display maths mode), this is especially helpful for integrals.

### Use `\small` for a smaller font

Use `$\small{text}$` when you need to display smaller fonts or fractions in your LaTeX expressions. For example, `$\small{\frac{1}{2}}$` will produce a smaller fraction than `$\frac{1}{2}$`.

$\small{\frac{1}{2}} \quad$ (small)

$\frac{1}{2}$

### Use `\begin{array}` to generate a compact table
    
    ```latex
    \begin{array}{|c|c|}
    \hline
    \theta_{2,0} & \theta_{1,L}\\
    \hline
    -6700 & 130.5641\\
    \hline
    -6600 & 161.6086\\
    \hline
    \end{array}
    ```

![Image showing a example of a table](images/table.png)

### Use `\begin{aligned}` to keep your working formatted nicely

    ```latex
    \begin{aligned}
    M_{d e f} &=\dfrac{1}{2}(M+M^T)\\
    & =\dfrac{1}{2} \begin{pmatrix} 4 & 14\\ -6 & -11 \end{pmatrix}+\begin{pmatrix} 4 & -6\\ 14 & -11 \end{pmatrix}\\
    & =\begin{pmatrix} 4 & 4\\ 4 & -11 \end{pmatrix}
    \end{aligned}
    ```

![Image showing a example of a algined working](images/aligned.png)

### Use `\left` and `\right` for equations with multiple brackets

This sizes the brackets correctly to the height of the equation.

    ```latex
    f(x)=\left (\frac{(\cos (x) -x) + i(\sin (x) - x)}{wi} \right)
    ```

![Image showing a example of a brackets](images/bracket.png)

This also works for `[ ]` and `\{ \}`

### Shortcut for romanised operators

Use `\sin`, `\cos`, etc. as a shortcut for `\text{sin }`, `\text{cos }`, etc.
