# Web App 
Math rendering in the web application has be designed to be as modular as possible. Every equation to be rendered calls the generic `Math` component. Furthermore, some libraries requires a provider to wrap the whole app, which is done by the `MathProvider`. So global imports and providers should be added to `MathProvider` and individual math rendering should be done in `Math`. 

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

### [katex](https://katex.org/)
Very fast, and widely used library. 

- Simple module API (`katex.render` or `katex.renderToString` for SSR)
- React-specific extensions exist (as linked on the [official](https://katex.org/docs/libs.html) katex website)
	- [react-latex](https://github.com/zzish/react-latex) (old and unmaintained)
	- [react-katex](https://github.com/talyssonoc/react-katex) (same)

#### Web App Implementation 
Coding in React is simple enough: 

```js
import { useEffect, useRef } from 'react'
import katex from 'katex'

export const Math = ({ tex, inline = false }) => {
  const eqn = useRef(null)

  useEffect(() => {
    katex.render(tex, eqn.current, {
      displayMode: !inline,
    })
  }, [eqn, inline, tex])

  return <span ref={eqn} />
}
```

- Options can easily be passed to the katex render method ([list](https://katex.org/docs/options.html))
- **IMPORTANT** The KaTeX css file needs to be imported!

#### Supported/Unsupported envs
- Doesn't support `\cancelto`, but does support `\cancel` ([link](https://katex.org/docs/supported.html#environments))