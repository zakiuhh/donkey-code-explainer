<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="assets/logo-light.png">
    <img alt="Donkey Code Explainer logo" src="assets/logo-light.png" width="140">
  </picture>
</p>

<h1 align="center">Donkey Code Explainer</h1>

<p align="center">
  A Claude skill that explains code in the dumbest-simple English possible,
  without changing what the code actually does.
</p>

---

## What it does

Paste code, say "explain this", and Claude breaks it into small blocks and explains each one in plain, friendly language. Loops, conditions, and math are traced with real numbers, so the logic actually clicks.

It is built for absolute beginners, but it never lies to keep things simple. The words get simpler, the truth stays the same.

## Modes

| Mode | Trigger | Result |
|---|---|---|
| **Whole** (default) | "explain this code" | Every block explained in one reply |
| **Step-by-step** | "one by one", "slowly" | One block at a time, pauses between |
| **Focus** | "explain just the loop" | Only that part, then stops |
| **Deep-dive** | "deep dive", "why this approach" | Adds the concept used, why it fits, and a traced walkthrough |

It also supports a **write-then-explain** flow: ask for a code exercise, and Claude writes the full code first, then explains it.

## Features

- Smart mode detection, so it only asks questions when it truly needs to
- Dry-run traces with real values for loops, conditions, recursion, and math
- Long-code handling: groups blocks, or gives a short map first for big files
- Language matching, including Hinglish
- Deep-dive mode that unpacks the concept and the reasoning behind it
- Flags bugs or risky lines in one plain sentence

## Example

Input:

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}
```

Output (short version):

> This is basically saying "do this 5 times." `i` is a counter that starts at 0. Each time around, it prints `i` and adds 1.
>
> ```
> i = 0 -> prints 0
> i = 1 -> prints 1
> i = 2 -> prints 2
> i = 3 -> prints 3
> i = 4 -> prints 4
> i = 5 -> 5 < 5 is false, loop stops
> ```

## Install

### Claude (web and apps)

1. Download this repo as a ZIP (or zip the `donkey-code-explainer` folder yourself). Make sure `SKILL.md` sits at the top level of the folder inside the ZIP.
2. Open Claude's settings and find the Skills section.
3. Upload the ZIP and turn the skill on.

### Claude Code

Copy the folder into your skills directory:

```bash
git clone https://github.com/zakiuhh/donkey-code-explainer.git
cp -r donkey-code-explainer ~/.claude/skills/
```

(Change the clone URL if your repo lives somewhere else.)

## Repo structure

```
donkey-code-explainer/
├── assets/
│   ├── logo-dark.png    # for dark backgrounds
│   └── logo-light.png   # for light backgrounds
├── LICENSE
├── README.md
└── SKILL.md             # the actual skill
```

## Customizing

All the behavior lives in `SKILL.md`. Edit the modes, the style rules, or the examples to fit how you like code explained. Keep the `name` in the frontmatter the same as the folder name.

## License

MIT. See [LICENSE](LICENSE).
