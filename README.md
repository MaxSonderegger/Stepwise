# Stepwise

A notebook that checks your maths line by line. Write each step of a solution on its own line. Stepwise checks it against the line above, explains what went wrong when a step is not equivalent, and can work out the rest of the solution for you.

Everything lives in one file, `index.html`. There is no build step and no server.

## What it does

- **Checks each step.** Algebra, trigonometry (including shorthand like `cos^2 x`), derivatives, integrals (including improper ones), limits, implicit differentiation and complex numbers. A line gets a ✓ or ✗, or ↳ when a step splits into cases and cannot be compared with the line above.
- **Explains mistakes.** For example "forgot the chain rule", "the left side was divided by 2 but the right side stayed the same", or "differentiating this gives 2 times the integrand".
- **Typesets your maths** as you write: fractions, exponents, roots, integrals and so on.
- **Solve offline** works out the rest with built-in rules and no AI: linear and quadratic equations, cubics and quartics (with exact radical roots), derivatives, many integrals (including by parts), limits, trig identities, simplification and implicit differentiation. It shows how long it took.
- **Solve ▸ and Next step** use Claude for everything else. They need your own API key (see below).
- A built-in **syntax guide**, LaTeX export, and multiple pages that are saved in your browser.

## Run it

**Option 1: GitHub Pages.** Turn on Pages for this repository and open the link.

**Option 2: on your computer.** Download `index.html` and open it in a browser. It needs an internet connection to load math.js, MathJax and the fonts. If your browser blocks anything when opened from a file, serve the folder instead:

```
python3 -m http.server 8000
```

then open `http://localhost:8000`.

## Using Claude (Solve ▸ and Next step)

1. Create an API key in the [Claude Console](https://platform.claude.com/). Use a separate key for this and set a spending limit.
2. In Stepwise, click **Claude key**, paste the key, and choose a model (the default is `claude-sonnet-5-5`; `claude-haiku-5-5` is faster and cheaper).
3. Click **Test** to check it, then **Save**.

Each press of Solve ▸ or Next step sends one request containing the lines on your page. You pay Anthropic for what you use.

### Security, please read

- The key is stored only in your browser (for the current tab, or on the device if you tick "Remember") and is sent only to `api.anthropic.com`. It is never written into the code or the repository.
- Anyone who can use your browser can read the key. Do not save it on a shared computer.
- Calling the API straight from a web page is only sensible when each person uses **their own** key. Do not put your own key into a page that other people will use. If you want to offer Claude to the public, run a small server that holds the key and have the page call that instead.
- The lines you solve with Claude are sent to Anthropic.

## Writing maths

Open **Syntax guide** in the app for every format. A few examples:

| Type | Meaning |
|---|---|
| `x^2`, `sqrt(x)`, `(x+1)/(x-1)` | powers, roots, fractions |
| `cos^2 x`, `sin 2x`, `log(x)` | trig shorthand, natural log |
| `d/dx(x^3*sin(x))` | derivative |
| `dy/dx`, `y'` | derivative of y (tick "Treat y as a function of x" for implicit differentiation) |
| `int(2x,x)=x^2+C` | indefinite integral |
| `int(x,x,0,2)` | definite integral (`inf` for infinity) |
| `ev(x^2/2,x,0,2)` | apply bounds to an antiderivative |
| `lim(sin(x)/x,x,0)` | limit |

Keep one step per line, and one answer per line (no "or" or ±; give each case its own line).

## How the checking works

Stepwise evaluates both lines at many random values and compares the results. For equations it asks whether the two lines are scaled versions of each other, so doing the same thing to both sides passes. Derivatives are computed symbolically, and integrals are checked by differentiating the answer or by numerical integration.

This is a numerical test, not a proof. In rare cases a wrong step can pass, and a correct step can fail when it only holds on part of the domain. Treat a ✓ as strong evidence, not certainty.

## Limits

- Solve offline handles polynomial equations up to degree 4 in one unknown, and integrals within its built-in rules. Anything harder needs Solve ▸.
- Improper integrals are evaluated numerically. A very slowly converging one may be reported as diverging.
- Steps written by Claude are checked like your own, but Claude can still make mistakes. Watch for ✗.
- There is no automated test suite yet. Contributions are welcome.

## Third-party libraries

Loaded from CDNs at runtime. Their licences apply to them.

- [math.js](https://mathjs.org/) (Apache-2.0)
- [MathJax](https://www.mathjax.org/) (Apache-2.0)
- [Figtree](https://fonts.google.com/specimen/Figtree) and [JetBrains Mono](https://www.jetbrains.com/lp/mono/) fonts (SIL Open Font License)

## Contributing

Issues and pull requests are welcome. Because the app is one file, keep changes self-contained, update `CHANGELOG.md`, and bump the version label (in the `<title>` and next to the heading) when you release.

## Licence

MIT. See [LICENSE](LICENSE).
