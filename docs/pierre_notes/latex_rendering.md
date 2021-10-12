# MathJax 
- [Mathjax in react component](https://gist.github.com/GiacoCorsiglia/1619828473f4b34d3d914a16fcbf10f3)
- Uses the mathjax [npm package](https://www.npmjs.com/package/mathjax)
- [nextjs theme?](https://theme-next.js.org/docs/third-party-services/math-equations)

## React Mathjax NPM Libraries 
### [react-mathjax](https://www.npmjs.com/package/react-mathjax)
Most "popular" package (14k downloads per week on npm), but last updated 3 years ago (old). 

- Equations flicker while typesetting, as in when the user opens the page, the equations are first shown unrendered and then it takes a little moment for mathjax to typeset them. 
- Requires app to be wrapped in a MathJax context provider 

### [mathjax-react](https://www.npmjs.com/package/mathjax-react)
Relatively unused package (800 downloads per week on npm), but last updated a year ago 

- Provides a standalone `MathComponent` to work with (no ContextProvider required)
- No easy way to add or remove LaTeX packages 
	- Doesn't work with `\begin{equation*}`, `\begin{align*}`, `\begin{matrix}`... 

