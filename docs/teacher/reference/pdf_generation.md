# PDF Generation

Lambda Feedback uses a single source to render content both in the browser and by PDF. The browser view uses katex to render LaTeX, which limits the scope of LaTeX that can be used. katex doesn't use traditional LaTeX packages, but emulates many of the popular packages:
[Package Emulation](https://github.com/KaTeX/KaTeX/wiki/Package-Emulation)

When a question is published by a teacher, a PDF copy is also generated. The PDF compilation process uses `xelatex` and the [Latex Template](https://github.com/lambda-feedback/pdf-generator/blob/main/src/template.latex) is public. The template installs relevant packages, and a list of packages is compiled below. This list will be updated as we receive more requirements from users.

## Supported packages when generating a PDF

| Package       | Description                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **amsmath**   | Provides essential mathematical features like aligned equations, matrices, and advanced math functions; fundamental for most LaTeX math.          |
| **amssymb**   | Adds extra mathematical symbols beyond the base LaTeX set.                                                                                        |
| **babel**     | Enables multilingual support with proper hyphenation and typographical conventions; allows switching languages within a document.                 |
| **biblatex**  | Manages bibliographies with advanced features and customization; more flexible than traditional packages like `natbib`.                           |
| **bidi**      | Enables bidirectional text support for mixing LTR and RTL scripts like Arabic and Hebrew.                                                          |
| **booktabs**  | Provides commands for professional-looking tables with proper spacing and design; discourages vertical rules.                                     |
| **bracket**   | Offers commands for properly sizing and aligning brackets in math environments.                                                                    |
| **cancel**    | Draws slashes through math expressions to indicate cancellation; useful for derivations.                                                           |
| **eurosym**   | Adds the Euro (€) symbol with options for appearance to integrate with fonts.                                                                      |
| **fixltx2e**  | Fixes bugs and improves LaTeX2e; useful for older distributions (deprecated in recent versions).                                                   |
| **fancyvrb**  | Enhances verbatim text with customization; useful for code listings with line numbers and styling.                                                 |
| **fontenc**   | Specifies font encoding; allows use of comprehensive encodings like T1 for accented characters.                                                    |
| **fontspec**  | Allows use of system fonts (OpenType, TrueType) with XeLaTeX/LuaLaTeX; offers advanced font selection.                                             |
| **geometry**  | Simplifies setting page dimensions, margins, and layout parameters.                                                                                |
| **graphicx**  | Includes and manipulates images in documents.                                                                                                      |
| **grffile**   | Allows inclusion of graphics with filenames containing multiple dots or spaces.                                                                    |
| **hyperref**  | Creates hyperlinks in documents; makes references, citations, and TOC entries clickable.                                                           |
| **ifxetex**   | Checks if document is compiled with XeTeX; useful for engine-specific configurations.                                                              |
| **ifluatex**  | Checks if document is compiled with LuaTeX; enables engine-specific configurations.                                                                |
| **inputenc**  | Specifies input encoding (e.g., UTF-8) for source files; allows direct typing of accented characters.                                              |
| **listings**  | Includes and formats source code with syntax highlighting and customization.                                                                       |
| **longtable** | Creates tables that span multiple pages with automatic breaks and repeated headers.                                                                |
| **lmodern**   | Provides the Latin Modern font family; improved version of default fonts with more characters.                                                     |
| **mathspec**  | Uses OpenType fonts for math in XeLaTeX/LuaLaTeX; matches math fonts with text fonts.                                                              |
| **microtype** | Improves typography with microtypographic extensions like character protrusion and font expansion.                                                 |
| **natbib**    | Advanced citation management; supports various styles and integrates with BibTeX.                                                                  |
| **parskip**   | Adds vertical space between paragraphs and removes indentation.                                                                                    |
| **pifont**    | Provides access to Dingbat fonts for symbols like checkmarks and crosses.                                                                          |
| **polyglossia** | Multilingual support for XeLaTeX/LuaLaTeX; provides language-specific typographical rules.                                                       |
| **setspace**  | Adjusts line spacing (single, one-and-a-half, double) in documents.                                                                                |
| **ulem**      | Adds advanced underlining and strikethrough styles; allows underlines to break at line ends.                                                       |
| **upquote**   | Ensures straight quotes in code listings; prevents conversion to curly quotes.                                                                     |
| **xcolor**    | Adds color to text and math expressions.                                                                                                           |
| **xeCJK**     | Typesets Chinese, Japanese, and Korean (CJK) characters in XeLaTeX; handles fonts, spacing, and line breaking.                                     |


