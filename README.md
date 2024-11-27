# Markdown-it Katex

> Add square brackets \\[...\\] and parentheses \\(...\\) support

Markdown it plugin that adds [KaTeX](https://github.com/Khan/KaTeX) rendering. This is used by VS Code to render math in markdown.

Need convincing?

* Check out the comparative benchmark: [KaTeX vs MathJax](https://jsperf.com/katex-vs-mathjax/42)

Originally forked from [@vscode/markdown-it-katex](https://github.com/microsoft/vscode-markdown-it-katex.git) and [@iktakahiro/markdown-it-katex](https://github.com/iktakahiro/markdown-it-katex)

## Usage 

Install markdown-it

```bash
npm install markdown-it
```

Install the plugin

```bash
npm install @chyi13/markdown-it-katex
```

Use it in your javascript

```javascript
var md = require('markdown-it')(),
    mk = require('@chyi13/markdown-it-katex').default;

// enableMathBlockLatex to enable square brackets \\[...\\] and parentheses \\(...\\) support
md.use(mk, { enableMathBlockLatex: true });

// double backslash is required for javascript strings, but not html input
var result = md.render('# Math Rulez! \n  $\\sqrt{3x-1}+(1+x)^2$');

// square brackets \\[...\\] and parentheses \\(...\\)
var result = md.render('\\[\n\\nabla \\times \\mathbf{B} = \\mu_0 \\mathbf{j} + \\mu_0 \\varepsilon_0 \\frac{\\partial \\mathbf{E}}{\\partial t}\n\\]');
```

Include the KaTeX stylesheet in your html:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.4/dist/katex.min.css">
```

If you're using the default markdown-it parser, I also recommend the [github stylesheet](https://github.com/sindresorhus/github-markdown-css):

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/4.0.0/github-markdown.min.css"/>
```

`KaTeX` options can be supplied with the second argument to use.

```javascript
md.use(mk, {"throwOnError" : false, "errorColor" : " #cc0000"});
```

## Examples

### Inline

Surround your LaTeX with a single `$` on each side for inline rendering.

```latex
$\sqrt{3x-1}+(1+x)^2$
```

### Block

Use two (`$$`) for block rendering. This mode uses bigger symbols and centers
the result.

```latex
$$\begin{array}{c}

\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &
= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\

\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\

\nabla \cdot \vec{\mathbf{B}} & = 0

\end{array}$$
```

## Syntax

Math parsing in markdown is designed to agree with the conventions set by pandoc:

    Anything between two $ characters will be treated as TeX math. The opening $ must
    have a non-space character immediately to its right, while the closing $ must
    have a non-space character immediately to its left, and must not be followed
    immediately by a digit. Thus, $20,000 and $30,000 won’t parse as math. If for some
    reason you need to enclose text in literal $ characters, backslash-escape them and
    they won’t be treated as math delimiters.

## Math Syntax Support

KaTeX is based on TeX and LaTeX. Support for both is growing. Here's a list of
currently supported functions:

[Things that KaTeX does not (yet) support](https://github.com/KaTeX/KaTeX/wiki/Things-that-KaTeX-does-not-%28yet%29-support)
