#programmeringsspråk 
# Markdown tips
- [Github Cheatsheet](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.md)
- PDF til Markdown-konverter  [PDF to Markdown Converter - Free Online Tool](https://notegpt.io/pdf-to-markdown-converter)

# Obsidian
[Mattetriks 1](https://github.com/ashu-otaku/Personal-Wiki) ([Reddit](https://www.reddit.com/r/ObsidianMD/comments/1ayyz9d/taking_maths_notes_in_obsidian/))
[How to Write Mathematical Notations in Obsidian](https://www.makeuseof.com/write-mathematical-notation-obsidian/)

>[!info]- Bilde
>![[IOS CLI-1.png]]

[Everything I wish I knew when starting to use Obsidian — Nicholas Seitz Photographer](https://www.nickseitz.com/writing/obsidian-day-one-starterpack)
[Fetching Title#sw5o](https://www.makeuseof.com/write-mathematical-notation-obsidian/)

## OneNote to markdown
[GitHub - ZeroClad/ink2excal](https://github.com/ZeroClad/ink2excal)

## MathJax
[LaTeX Cheat Sheet & Quick Reference](https://quickref.me/latex)
[GitHub - artisticat1/obsidian-latex-suite: Make typesetting LaTeX as fast as handwriting through snippets, text expansion, and editor enhancements](https://github.com/artisticat1/obsidian-latex-suite)

```
$$
Na + Cl \rightarrow Na^+ + Cl^- \rightarrow NaCl
$$
```
$$
Na + Cl \rightarrow Na^+ + Cl^- \rightarrow NaCl
$$

### Reference
[MathJax basic tutorial and quick reference - Mathematics Meta Stack Exchange](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
1. **For inline formulas, enclose the formula in `$`…`$`. For displayed formulas, use `$$`…`$$`.**
    - These render differently. For example, type the following to show _inline_ mode:  
        `$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$`  
        ∑ni=0i2=(n2+n)(2n+1)6

- or type the following for display mode:  
    `$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$`  
    
    ∑i=0ni2=(n2+n)(2n+1)6
    

- For **Greek letters**, use `\alpha`, `\beta`, …, `\omega`: α
    
, β, …, ω

.

- For uppercase letters, use `\Gamma`, `\Delta`, …, `\Omega`: Γ

, Δ, …, Ω- .
- Other Greek capital letters are the same as the Latin ones: `A,B,E,Z` and so on: A,B,E,Z
- ….
- Some Greek letters have variant forms: `\epsilon \varepsilon` ϵ
, ε, `\phi \varphi` ϕ, φ- - , and others.
- For **superscripts and subscripts**, use `^` and `_`. For example, `x_i^2`: x2i
    
, `\log_2 x`: log2x. For the **prime** symbol, use an apostrophe `x' x'' x'''`: x′ x′′ x′′′- .
    
- **Groups**. Superscripts, subscripts, and other operations apply only to the next “group”. A “group” is either a single symbol, or any formula surrounded by curly braces `{`…`}`.
    
    - If you do `10^10`, you will get a surprise: 1010
. But `10^{10}` gives what you probably wanted: 1010- .
- Use curly braces to delimit a formula to which a superscript or subscript applies: `x^y^z` is an error; `{x^y}^z` is xyz
, and `x^{y^z}` is xyz. Observe the differences between `x_i^2` x2i, `x_{i^2}` xi2 and `{x_i}^2` xi2- - .
- **Parentheses** Ordinary symbols `()[]` make parentheses and brackets (2+3)[4+4]
    
. Use `\{` and `\}` for curly braces {}

.

- These do _not_ scale with the formula in between, so if you write `(\frac{\sqrt x}{y^3})` the parentheses will be too small: (x√y3)
    

. Using `\left(`…`\right)` will make the sizes adjust automatically to the formula they enclose: `\left(\frac{\sqrt x}{y^3}\right)` is (x√y3)- .
    
- `\left` and`\right` apply to all the following sorts of parentheses: `(` and `)` (x)
    
, `[` and `]` [x], `\{` and `\}` {x}, `|` |x|, `\vert` |x|, `\Vert` ∥x∥, `\langle` and `\rangle` ⟨x⟩, `\lceil` and `\rceil` ⌈x⌉, and `\lfloor` and `\rfloor` ⌊x⌋. `\middle` can be used to add additional dividers. There are also invisible parentheses, denoted by `.`: use `\left.x^2\right\rvert_3^5 = 5^2-3^2` to get

x2∣∣53=52−32

- **Sums and integrals** `\sum` and `\int`; the subscript is the lower limit and the superscript is the upper limit, so for example `\sum_1^n` ∑n1
    
. Don't forget `{`…`}` if the limits are more than a single symbol. For example, `\sum_{i=0}^\infty i^2` is ∑∞i=0i2

.

- Similarly, `\prod` ∏

, `\int` ∫, `\bigcup` ⋃, `\bigcap` ⋂, `\iint` ∬, `\iiint` ∭, `\idotsint` ∫⋯∫- - .
- **Fractions** There are [three ways to make fractions](https://math.meta.stackexchange.com/questions/12978/should-dfrac-be-edited-in). `\frac ab` applies to the next two groups, and produces ab
    
; for more complicated numerators and denominators use `{`…`}`: `\frac{a+1}{b+1}` is a+1b+1

.

- If the numerator and denominator are complicated, you may prefer `\over`, which splits up the group that it is in: `{a+1\over b+1}` is a+1b+1

1. - .
    - For continued fractions, [use `\cfrac` instead of `\frac`](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference/5058#5058).
2. **Fonts**
    

- Use `\mathbb` or `\Bbb` for "blackboard bold": CHNQRZ

- .
- Use `\mathbf` for boldface: CHNQRZ
chnqrz.

- For expression based characters, use `\boldsymbol` instead: α

- Use `\mathit` for italics: CHNQRZ
chnqrz- .
- Use `\pmb` for boldfaced italics: CHNQRZCHNQRZ
chnqrzchnqrz- .
- Use `\mathtt` for "typewriter" font: CHNQRZ
chnqrz- .
- Use `\mathrm` for roman font: CHNQRZ
chnqrz- .
- Use `\mathsf` for sans-serif font: CHNQRZ
chnqrz- .
- Use `\mathcal` for "calligraphic" letters: CHNQRZ
- (Uppercase only.)
- Use `\mathscr` for script letters: CHNQRZ
chnqrz

- Use `\mathfrak` for "Fraktur" (old German style) letters: CHNQRZ
chnqrz

- .

9. **Radical signs / roots** Use `sqrt`, which adjusts to the size of its argument: `\sqrt{x^3}` x3−−√
    

; `\sqrt[3]{\frac xy}` xy−−√3- . For complicated expressions, consider using `{...}^{1/2}` instead.
    
- Some **special functions** such as "lim", "sin", "max", "ln", and so on are normally set in roman font instead of italic font. Use `\lim`, `\sin`, etc. to make these: `\sin x` sinx
    
, not `sin x` sinx. Use subscripts to attach a notation to `\lim`: `\lim_{x\to 0}`

limx→0

Nonstandard function names can be set with `\operatorname{foo}(x)` foo(x)- .
    
- There are a very large number of **special symbols and notations**, too many to list here; see the short listing [LATEX](https://pic.plover.com/MISC/symbols.pdf)
    
[and AMS](https://pic.plover.com/MISC/symbols.pdf)[-LATEX](https://pic.plover.com/MISC/symbols.pdf) [Symbols](https://pic.plover.com/MISC/symbols.pdf) prepared by Dr. Emre Sermutlu, or the exhaustive listing [The Comprehensive LATEX](https://www.ctan.org/tex-archive/info/symbols/comprehensive/symbols-a4.pdf)

9. [Symbol List](https://www.ctan.org/tex-archive/info/symbols/comprehensive/symbols-a4.pdf) by Scott Pakin. Some of the most common include:
    

- `\lt \gt \le \ge \neq` <
    

, >, ≤, ≥,≠. You can use `\not` to put a slash through almost anything: `\not\lt` ≮- but it often looks bad.
    
- `\times \div \pm \mp` ×
    
, ÷, ±, ∓. `\cdot` is a centered dot: x⋅y

- `\cup \cap \setminus \subset \subseteq \subsetneq \supset \in \notin \emptyset \varnothing` ∪
    
, ∩, ∖, ⊂, ⊆, ⊊, ⊃, ∈, ∉, ∅, ∅

- `{n+1 \choose 2k}` or `\binom{n+1}{2k}` (n+12k)
    

- `\to \gets \rightarrow \leftarrow \Rightarrow \Leftarrow \mapsto \implies \iff` →
    
, ←, →, ←, ⇒, ⇐, ↦, ⟹, ⟺

- `\land \lor \lnot \forall \exists \top \bot \vdash \vDash` ∧
    
, ∨, ¬, ∀, ∃, ⊤, ⊥, ⊢, ⊨

- `\star \ast \oplus \circ \bullet` ⋆
    
, ∗, ⊕, ∘, ∙

- `\approx \sim \simeq \cong \equiv \prec \lhd` ≈
    
, ∼, ≃, ≅, ≡, ≺, ⊲

- `\infty \aleph_0` ∞ℵ0
    
`\nabla \partial` ∇, ∂ `\Im \Re` I, R

- For modular equivalence, use `\pmod` like this: `a\equiv b\pmod n` a≡b(modn)
    
. For the binary mod operator, use `\bmod` like this: `a\bmod 17` amod17- .
    
- Use `\dots` for the triple dots in a1,a2,…,an
    
and a1+a2+⋯+an

- Script lowercase l is `\ell` ℓ
    

.

[Detexify](https://detexify.kirelabs.org/classify.html) lets you draw a symbol on a web page and then lists the TEX

symbols that seem to resemble it. These are not guaranteed to work in MathJax, but it's a good place to start. To check that a command is supported, note that MathJax.org maintains a [list of currently supported LATEX](https://docs.mathjax.org/en/latest/input/tex/macros/index.html) [commands](https://docs.mathjax.org/en/latest/input/tex/macros/index.html), and one can also check Dr. Carol JVF Burns's page of [TEX](https://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm)

- [Commands Available in MathJax](https://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm).
    

12. **Spaces** MathJax usually decides for itself how to space formulas, using a complex set of rules. Putting extra literal spaces into formulas will not change the amount of space MathJax puts in: `a␣b` and `a␣␣␣␣b` are both ab
    

. To add more space, use `\,` for a thin space ab; `\;` for a wider space ab. `\quad` and `\qquad` are large spaces: ab, ab

.

To set plain text, use `\text{…}`: {x∈s∣x is extra large}

- . You can nest `$…$` inside of `\text{…}`, for example to access spaces.
    
- **Accents and diacritical marks** Use `\hat` for a single symbol x^
    
, `\widehat` for a larger formula xyˆ. If you make it too wide, it will look silly. Similarly, there are `\bar` x¯ and `\overline` xyz¯¯¯¯¯¯¯¯, and `\vec` x⃗  and `\overrightarrow` xy−→ and `\overleftrightarrow` xy←→. For dots, as in ddxxx˙=x˙2+xx¨- , use `\dot` and `\ddot`.
    
- Special characters used for MathJax interpreting can be escaped using the `\` character: \$ $
    
, `\{` {, `\}` }, `\_` _, `\#` #, `\&` &. If you want `\` itself, you should use `\backslash` (symbol) or `\setminus` ([binary operation](https://tex.stackexchange.com/questions/511328/difference-between-commands-setminus-and-backslash/511332#511332)) for ∖

12. , because `\\` is for a new line.
    

(Tutorial ends here.)

---

It is important that this note be reasonably short and not suffer from too much bloat. To include more topics, please create short addenda and post them