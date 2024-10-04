# PDF Generation

## Supported packages

amsmath: This package is essential for many mathematical features, including aligned equations, matrices, and more advanced math functions. It’s fundamental to most LaTeX documents involving mathematics.

amssymb: Provides additional mathematical symbols not covered by the base LaTeX distribution.

babel: Provides multilingual support in LaTeX documents. It allows you to typeset documents in various languages, providing proper hyphenation, date formats, and typographical conventions. It also enables you to switch between languages within the same document.

biblatex: Is used for managing bibliographies in LaTeX documents. It offers advanced features for creating, formatting, and referencing bibliographic data. It provides more flexibility compared to traditional bibliography packages like natbib, allowing for extensive customization of citations and bibliography styles.

bidi: Provides bidirectional text support in LaTeX. It is essential for typesetting documents that contain both left-to-right (LTR) and right-to-left (RTL) text, such as Arabic, Hebrew, Persian, and Urdu. It handles the complexities of mixing LTR and RTL scripts in the same document.

booktabs: Enhances the quality of tables in LaTeX documents by providing additional commands for creating professionally styled tables. It focuses on the design and spacing of horizontal lines, helping to produce tables that adhere to high typographic standards without vertical rules, which are generally discouraged in professional typesetting.

bracket: Is designed to handle specific types of brackets in mathematical environments. It provides commands to properly size and align brackets, ensuring that they scale correctly with the content they enclose, which is particularly useful in complex mathematical expressions.

cancel: Is used to draw diagonal lines (“slashes”) through mathematical expressions, indicating cancellation. This is useful in demonstrating steps in mathematical derivations where terms are canceled out. The package provides commands for different styles of cancellation (e.g., diagonal, cross out).

eurosym: Provides the Euro currency symbol (€) in LaTeX documents. It offers several options for the appearance of the symbol, ensuring that it integrates well with various fonts and typographical styles used in the document.

fixltx2e: Provides fixes for bugs and improvements in the standard LaTeX2e distribution. It is particularly useful for older LaTeX distributions to ensure compatibility and correct behavior of certain commands. Note that in more recent LaTeX distributions, this package is deprecated as its fixes have been incorporated into LaTeX itself.

fancyvrb: Provides enhanced functionality for typesetting verbatim text in LaTeX. It allows for customization of verbatim environments, including changing fonts, adding line numbers, and creating shaded backgrounds. It is useful for typesetting code listings or any text that should be displayed exactly as typed.

fontenc: Is used to specify the font encoding in LaTeX documents. Font encoding defines how characters are represented in the output. By default, LaTeX uses a limited encoding (OT1), but fontenc allows you to switch to more comprehensive encodings like T1, which supports accented characters and other symbols, making the document suitable for European

fontspec: Is used in conjunction with XeLaTeX or LuaLaTeX to load OpenType, TrueType, and other system fonts in LaTeX documents. It provides advanced font selection and configuration features, allowing you to use any font installed on your system with LaTeX, offering greater flexibility and typographic control.

geometry: Simplifies the task of setting page dimensions in LaTeX documents. It allows you to specify margins, paper size, and other page layout parameters easily. This package is particularly useful for adjusting the layout to meet specific formatting requirements or to create custom-sized documents.

graphicx: For including and manipulating images, which is relevant if you want to include things like scalable vector graphics that KaTeX also supports in some setups.

grffile: Extends the file name handling capabilities in LaTeX, allowing for the inclusion of graphics with filenames containing multiple dots or spaces. It is particularly useful when working with image files that have complex names, ensuring LaTeX can correctly locate and render them.

hyperref: Is used to create hyperlinks within a LaTeX document, enhancing navigation in PDFs. It automatically converts references, citations, and table of contents entries into clickable links. It also allows you to create custom hyperlinks to URLs, files, and internal document locations.

ifxetex: Provides a simple conditional command that allows you to check if your document is being compiled with XeTeX. It is often used in conjunction with ifluatex to create documents that are compatible with multiple LaTeX engines (e.g., pdfTeX, XeTeX, LuaTeX).

ifluatex: Provides a conditional command that allows you to check if your document is being compiled with LuaTeX. It helps ensure compatibility across different LaTeX engines by enabling engine-specific configurations.

inputenc: Allows you to specify the input encoding of your LaTeX document, which determines how characters in your source file are interpreted. For example, using \usepackage[utf8]{inputenc} allows you to directly type accented characters and special symbols in UTF-8 encoding. Note that in more recent versions of LaTeX, inputenc is no longer necessary for UTF-8, as it is handled natively.

listings: Provides tools for including and formatting source code in LaTeX documents. It supports syntax highlighting for many programming languages and allows customization of font styles, colors, line numbers, and other aspects of code presentation, making it ideal for technical documents or publications involving code.

longtable: Allows you to create tables that span multiple pages in a LaTeX document. It automatically breaks the table across pages, repeating the header and/or footer rows as needed, which is particularly useful for documents containing large datasets or extensive tabular information.

lmodern: Provides the Latin Modern font family, an enhanced version of the Computer Modern fonts that are the default in LaTeX. lmodern includes additional characters and glyphs, supporting better scalability and compatibility with modern typographic standards.

mathspec: Allows you to use OpenType fonts for typesetting mathematics in XeLaTeX and LuaLaTeX. It enables the selection of different fonts for math mode, offering more typographic flexibility and the ability to match math fonts with text fonts.

microtype: Enhances the typographic quality of LaTeX documents by enabling microtypographic extensions like character protrusion and font expansion. These techniques improve justification, spacing, and overall visual appeal of the text, especially in justified paragraphs.

natbib: Provides advanced citation management for LaTeX documents. It offers various citation styles, supports both author-year and numerical citations, and integrates well with the standard bibtex bibliography system. It is widely used in academic writing to control citation and bibliography formatting.

parskip: Changes the way paragraphs are formatted in LaTeX by adding vertical space between paragraphs and eliminating indentation. It is useful when a document’s design calls for a clear separation between paragraphs rather than the traditional indentation.

pifont: Allows the use of Dingbat fonts in LaTeX documents. It provides easy access to various symbol fonts, including the popular Zapf Dingbats, which are useful for adding checkmarks, crosses, and other decorative symbols to your document.

polyglossia: Is the multilingual package for XeLaTeX and LuaLaTeX, similar to babel but specifically designed for modern LaTeX engines. It provides language-specific typographical rules, hyphenation patterns, and more, enabling the seamless integration of multiple languages in a single document.

setspace: Provides tools to adjust the spacing between lines in a LaTeX document. It allows you to easily switch between single, one-and-a-half, and double line spacing, either globally or locally within a document, which is often required in academic or formal writing.

ulem: Provides various types of underlining in LaTeX, such as single, double, wavy, or dotted underlines. It also offers commands for striking out text. Unlike the standard \underline command, ulem allows underlines that break at line ends, making it more flexible for text decoration.

upquote: Ensures that straight quotes (' and ") are typeset as they appear in code listings or verbatim text, rather than being converted to curly quotes. This is particularly important when including code snippets where the distinction between straight and curly quotes is semantically significant.

xcolor: For coloring text and math expressions, which KaTeX supports natively.

xeCJK: Is specifically designed for typesetting documents that include Chinese, Japanese, and Korean (CJK) characters in XeLaTeX. It provides better handling of CJK fonts, enabling proper spacing, line breaking, and font selection for these languages. The package integrates seamlessly with XeLaTeX’s ability to use system fonts, allowing for high-quality typesetting of multilingual documents that include both CJK and Latin scripts. xeCJK also offers various options for fine-tuning the appearance of CJK text, such as adjusting character spacing and font sizes.


## List of LaTex packages emulated by KaTeX

[Package Emulation](https://github.com/KaTeX/KaTeX/wiki/Package-Emulation)
