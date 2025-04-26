(C) 2024 Swudu Susuwu, dual licenses: choose [_GPLv2_](./LICENSE_GPLv2) or [_Creative Commons Attribution 2_](./LICENSE) (allows all uses).

# Table of Contents
- [How to use this](#how-to-use-this)
  - [Download](#download)
- [How to contribute](#how-to-contribute)
  - [Beta test/experimental branch](#beta-testexperimental-branch)
  - [Good first issues to contribute to](https://github.com/SwuduSusuwu/SusuPosts/contribute)
  - [Contributor conventions/rules](#contributor-conventionsrules)
    - [_Markdown_](#markdown)
    - [`git`](#git)
  - [Sponsor](#sponsor)
    - [Escrow](#escrow)
    - [Affiliates](#affiliates)

# How to use this
This repo is new. So that fixes do not require use of `git push --force` on the [`trunk`](https://github.com/SwuduSusuwu/SusuPosts/tree/trunk/) branch (or tons of trivial fixes which bloat `git log`), new posts go to the [`preview`](https://github.com/SwuduSusuwu/SusuPosts/tree/preview/) branch for review (which can last months).
- For now, just the `preview` branch has posts.
## Download
Download with `git clone https://github.com/SwuduSusuwu/SusuPosts.git` and browse local with `cd mid/ && ls`.
- To opt-in to the beta (the preview), use `git switch preview` (opt-out with `get switch trunk`).

# How to contribute
View [documented issues](https://github.com/SwuduSusuwu/SusuPosts/issues/) (for ideas on how to contribute, plus so you do not report documented issues.)
## Beta test/`experimental` branch
- `git switch experimental`
  - Preview samples / scripts symptoms of new issues (hint: listen to samples for glitches, or look through script outputs for "Warning:"s or "Error:"s).
  - If you found new issue(s) (which aren't due to misconfigurations in your system), [post new issue(s)](https://github.com/SwuduSusuwu/SusuPosts/issues/new).
    - Notice: [sensitive issue(s)](./SECURITY.md#sensitive-issues) have a separate protocol.

# Contributor conventions/rules
General comment/message syntax rules: `<>` goes around type of option/argument (such as `<commit-hash>`, `[]` goes around optional comments/options/arguments (such as `[<optional fallback value>]`, `...` is affixed to allow multiple options/arguments (such as `[; optional extra arguments]...`). This rule is used to document function arguments (such as `sh`, `C` or `C++` use), plus to document `git` uses.
To ensure consistent code, submissions of code (such as through [pull requests](https://github.com/SwuduSusuwu/SusuPosts/pulls)) have language-specific syntax rules:
## _Markdown_
`` *.md `` shall use:
- [_GitHub flavored Markdown_](https://github.github.com/gfm/), which is not just compatible with [_GitHub_](https://github.com) but also:
  - Has lots of [unit tests](https://wikipedia.org/wiki/Unit_test#Agile). Most of the differences from the original _Markdown_ are just so rules are less ambiguous.
  - Is close to the original _Markdown_ (thus compatible with most _Markdown_ tools, such as [`glow`](https://github.com/charmbracelet/glow?tab=readme-ov-file#glow)).
- [_ISO 8601_](https://wikipedia.org/wiki/ISO_8601), which
  - Is the most popular national standard format.
  - Versus formats which use locale-dependent names of months, is more portable and less ambiguous.
  - Versus formats which use backslashes, is more portable (filesystem paths can include).
- [_Unix_](https://wikipedia.org/wiki/Unix) paths start with `./` (if relative) or `/` (if absolute), so that [`sed`](https://manpages.org/sed) (and [`grep`](https://manpages.org/grep)) [performance is improved](https://poe.com/s/NX7kVKtCL9k04WIqieoh).
  - That is, paths shall match the [Regular Expression](https://wikipedia.org/wiki/Regular_expression) `^\.*\/[\w]*` (more than 1 `.` is allowed).
  - [_Microsoft Windows_](https://wikipedia.org/wiki/Microsoft_Windows) can use _Unix_ paths, except that absolute paths must start with the drive prefix (`[A-Z]:/` versus `/`).
  - [_HTTP_](https://wikipedia.org/wiki/HTTP) can use _Unix_ paths, except that absolute paths must start with the protocol (`http[s]*://` versus `/`).
## `git`
If `git commit` introduces/removes functions, have `./README.md#purposes` include this.
Do atomic commits: if swapping the new commit with a previous commit (such as through `git rebase -i`) -- or if `git revert` of a previous commit -- causes  `./build.sh` to return a non-0 exit status, `git commit`'s message shall include such as:
> Is followup to: \<ref | commit-hash\> \(\<commit-message\>\)\[, comment\] \[; \<ref | commit-hash\> \(\<commit-message\>\)\[, comment\]\]...

- This shows the temporal order of commits required for `./build.sh` to pass.
- `<commit-message>` is so that `git rebase` (which changes `<commit-hash>`) does not make it impossible to follow (plus, so comments are reduced), thus you should use the exact message. You can use ellipsis (`...`) to omit extra lines, but it is best if the first line is exact (left as-is).
- This format allows comments to include `<commit-hash>`'s and `,`'s (just not `;`'s).

`git commit` message format/syntax:
- affix "()" onto functions (regardless of number of arguments), such as `function()`, or use the function name (such as `function`) alone.
- if commit does `git add NewFile`: message has `+\`NewFile\``.
- if `git rm Exists`: `-\`Exists\``.
- if `touch Exists && git add Exists`: `@\`Exists\`` or `?\`Exists\``.
  - Simple wildcards/regex for altered functions: `\`%s/oldFunction()/newFunction()/\``.
  - '*' is not used as update prefix, since '*' has much other use in _Regex_ (wildcards) & _C++_ (such as block comments, dereferences, or math).
    - From the root commit through 159940fb8b60b176a38a13cdfbd9393596daa9b5 (Date:   Thu Jul 4 07:56:01 2024 -0700), '@' was the prefix for updates. From then until this commit, '?' was the prefix for updates.
    - From this commit on (this is the successor to commit 0ae6233c02d9e04fca60027b1e32b885eb69bb8a (Date:   Sat Nov 30 17:50:40 2024 -0800)), '@' is (once more) the prefix for updates, due to: it is more common for projects to so use '@'.
- if `echo "int newFunction() {...}" >> Exists && git add Exists`: `@\`Exists\`:+\`NewFunction()\``.
- if `git mv OldPath/ NewPath/`: `\`OldPath/\` -> \`NewPath/\`` or `mv OldPath/ NewPath/`.
- as default branch, choose `master`, `main` or `trunk` (do not have more than 1 of those branches, or [`./Macros.sh:SUSUWU_DEFAULT_BRANCH()`](./Macros.sh) is ambiguous).
- to indent: use tabs to form blocks, such as:
```
?`README.md`:
	?`#How-to-use-this`:
	Split into:
		+`## Download`: new; howto clone, howto switch branches.
		+`## Optionssetup`: "Options/setup"; howto use `./build.sh` (with or without options.)
	?`#How-to-contribute`,
	?[Good first issues to contribute to]: (moved into `#How-to-contribute`)
```
/[Notice: Commit titles can omit backticks (``) if not enough room; the backticks just allow _GitHub_ to do _Markdown_-format code/paths.\]
## Sponsor
To sponsor this (which allows us to produce more source codes), you can use crypto (such as [**Bitcoin**](https://wikipedia.org/wiki/Bitcoin)) to [produce a one-time-use address](https://poe.com/s/IPhIMyuMY6SnYM0yqEJl) (which you deposit funds into), and send the address&private-key to [a contact which `./SECURITY.md` lists](./SECURITY.md#sensitive-issues).
- Rather than us publish a send-to address (for a particular protocol), this allows us to accept all forms of crypto.
### Escrow
If you want proof that your crypto/cash will go to produce specific systems, use [**escrow** services](https://wikipedia.org/wiki/Escrow) (what you send the **escrow** is: crypto/cash, plus contract which references an [open issue which you choose](https://github.com/SwuduSusuwu/SusuPosts/issues/)).
- If none of those issues match what you want, you can [post your own issue](https://github.com/SwuduSusuwu/SusuPosts/issues/new) for this.
- Ensure that the **escrow** contract includes specifics as to what will count as "issue closed" [to the **escrow** service (so you do not have to trust the author),](https://wikipedia.org/wiki/Online_dispute_resolution) which will release the crypto/cash (once the **escrow** service considers your issue as closed).
  - For example; "The **source code** (through `./build.sh`), must produce a **system** (a **shared object** or **executable**) which uses just half of the training data to [setup its neural network, which must produce virtual synapses](https://wikipedia.org/wiki/Backpropagation) which the **system** [uses to produce **accurate** results](https://wikipedia.org/wiki/Residual_neural_network#Forward_propagation) on the other half, where **accurate** (for [classifiers](https://wikipedia.org/wiki/Learning_classifier_system)) is less than 2% false negatives and less than 2% false positives, and **accurate** (for [generators](https://wikipedia.org/wiki/Generative_artificial_intelligence)) is [divergence](https://wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) of less than 2%." is a contract which an **escrow** can use for [issue #6](https://github.com/SwuduSusuwu/SusuLib/issues/6).
### Affiliates
You can use [_Capital 1_'s affiliate program](https://i.capitalone.com/JgR02Y4pE) to allow us to publish more for you.

