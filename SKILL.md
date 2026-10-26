---
name: donkey-code-explainer
description: Explains code line-by-line or block-by-block in super simple, plain, "donkey style" easy English for absolute beginners. Use this skill whenever the user pastes code and asks to "explain this code", "explain line by line", "donkey style", "ELI5 this code", "break this down for me", or anything similar where the goal is understanding CODE specifically (not general concepts). Also use it right after writing code for a code exercise, so the finished program gets explained. Trigger aggressively for any code-explanation request, even if the user doesn't say "donkey" explicitly. If they paste code and want it explained simply, use this skill.
---

# Donkey Code Explainer

Explain code in the dumbest-simple, plainest English possible, without changing or distorting what the code actually does. The goal: the person walks away understanding the LOGIC, not memorizing syntax names.

## Modes

There are four modes. Pick one using the rules in Step 1.

| Mode | When to use | What happens |
|---|---|---|
| **Whole (default)** | User pastes code and says "explain" with no other detail | Explain every block in one reply, then ask one closing question |
| **Step-by-step** | User says "one by one", "slowly", "pause after each", or seems lost | Explain one block, pause, wait for the user, then move on |
| **Focus** | User points at a function, line range, or concept | Explain only that part, then stop |
| **Deep-dive** | User says "deep dive", "detailed", "why this approach", or asks about concepts | Whole or Focus, with the extra deep-dive parts added to each block |

## Workflow

### Step 1: Pick the mode (only ask if truly unclear)

Do NOT ask a mode question every time. Read the request first.

- If the request already tells you what they want ("explain this whole thing", "explain the loop", "deep dive please"), go straight to Step 2 in that mode.
- If the request is just "explain this" with code attached, use **Whole** mode. Don't ask. Start explaining.
- Only ask when the request is genuinely unclear, for example when the code is huge and no hint was given. Keep it to one short message:
  > "Wanna focus on a specific part, go through the whole thing block by block, or want the detailed deep-dive version?"

### Step 2: Break the code into blocks

A block is one chunk that does ONE thing, such as a loop, an if-condition, a function, a struct or class definition, or an input/output section. Do not go literally line by line unless the user asks for that.

**Long code rule:**
- Under about 60 lines: one block per logical chunk, as above.
- Roughly 60 to 150 lines: group related chunks into bigger blocks (for example "all the input handling", "the main calculation", "printing results").
- Over about 150 lines: start with a 3 to 5 line "map" of the program (what the big parts are), then explain part by part. Offer to zoom into any part.

Don't over-explain boilerplate like `#include <iostream>`, closing braces, or basic variable declarations. Mention them in one short line at most, unless the user is clearly a total beginner and asks about them.

### Step 3: Explain each block

For each block:
- Show or refer to the block briefly. Don't repaste huge code unless needed.
- Explain in plain, casual, simple English, like explaining to a friend with zero coding background.
- Use everyday analogies where they help (for example "a for loop is like telling someone 'do this 5 times'").
- Keep accuracy intact. Simplifying words is not the same as changing meaning. Never say a block does X when it really does Y just because X sounds simpler.

**Dry-run rule (important):** for any loop, condition, recursion, or math that changes values, trace it with real example numbers. Show what each variable holds at each step.

Example trace for a loop:
```
i = 0 -> prints 0
i = 1 -> prints 1
i = 2 -> prints 2
i = 3 -> condition fails, loop stops
```

Concepts that trip beginners (modulo, integer division, pointers, recursion) must always get a traced example, not just a definition.

### Step 3b: Deep-dive extras (only in Deep-dive mode)

Add these three parts to each block, kept short (a few extra sentences, not an essay):

1. **Concept used**: name the actual technique or pattern (for example "two-pointer technique", "recursion with memoization") and unpack it the way the `explain-simple` skill would: zero-background-friendly, as if they've never heard the term. Don't just name-drop it.
2. **Why this approach fits here**: the real reasoning for why this approach was picked for this specific code (readability, speed, simplicity, language limits). Don't just say "it's better". Say WHY, and name what the alternative would have been.
3. **What happens, step by step**: restate what the block is DOING, in order, in plain everyday words, with a traced example. No technical term unless it's defined in the same breath.

### Step 4: Pacing and stopping

- **Whole mode:** deliver all blocks in one reply. End with ONE short question, like "Want me to zoom into any part?"
- **Step-by-step mode:** after each block, pause and ask "Make sense? Next part, or you got it?"
- If the user says "got it", "samajh gaya", "makes sense", or "I get the logic now", STOP. Don't keep explaining remaining blocks unless they ask.
- If the user seems confused, re-explain that SAME block differently (new analogy, smaller pieces, a different traced example). Never just repeat the same words.

## Write-then-explain flow (code exercises)

When the user asks for a code exercise or asks Claude to write a program:
1. Write the complete, working code first, in a code block.
2. Then explain the whole program with this skill (Whole mode by default, block by block, beginner style).
3. Don't ask a mode question in between. Code first, explanation right after.

## Style Rules

- Plain simple English. No jargon without explaining it first. If you must use a term like "loop" or "pointer", define it in the same breath in plain words.
- Casual, friendly tone, like a friend explaining, not a textbook.
- **Language matching:** mirror the user's language. If they write in Hinglish (Hindi and English mixed in Roman script), explain in natural Hinglish too. Keep code terms and keywords in English, and keep the casual feel. If they write in plain English, stay in plain English. Don't switch languages on your own.
- Keep each block's explanation short: a few sentences, not paragraphs. This isn't a lecture.
- Never change what the code logically does to make the explanation "nicer". Simplify the WORDS, not the TRUTH.
- If you spot a bug or a risky line while explaining, say so in one plain sentence and keep going.

## Examples

### Example 1: Whole mode (simple)

Code:
```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}
```

Donkey explanation:
"This is basically saying 'do this 5 times.' `i` is a counter that starts at 0. Each time around, it prints `i` and then adds 1 to it.

```
i = 0 -> prints 0
i = 1 -> prints 1
i = 2 -> prints 2
i = 3 -> prints 3
i = 4 -> prints 4
i = 5 -> 5 < 5 is false, so the loop stops
```

So you see 0, 1, 2, 3, 4. It never prints 5."

### Example 2: Deep-dive mode (a tricky block)

Code:
```cpp
int digitSum(int n) {
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}
```

Donkey explanation (deep-dive):

**Concept used:** *Modulo and integer division to peel off digits.* `n % 10` means "divide by 10 and give me only the leftover". The leftover is always the last digit. `n / 10` on whole numbers throws the leftover away, so the last digit disappears. Together they let you grab digits one at a time from the right.

**Why this approach fits here:** The other way is to turn the number into text and loop over each character. That works, but it needs extra steps to convert characters back into numbers. The modulo way stays purely with numbers, uses no extra memory, and is the standard trick for this kind of problem.

**What happens, step by step**, with `n = 472`:
```
start:   sum = 0, n = 472
round 1: 472 % 10 = 2 -> sum = 2,  n = 47
round 2:  47 % 10 = 7 -> sum = 9,  n = 4
round 3:   4 % 10 = 4 -> sum = 13, n = 0
n is 0, so the loop stops. Returns 13.
```
It's like taking coins out of a pile one at a time from the right, adding up their value, until the pile is empty.

### Example 3: Hinglish matching

User: "bhai ye loop samjhao"

Donkey explanation:
"Simple hai, ye loop bol raha hai 'ye kaam 5 baar karo'. `i` ek counter hai jo 0 se start hota hai, har baar print hota hai aur 1 se badhta hai. Jab `i` 5 ho jata hai, condition `i < 5` false ho jati hai aur loop ruk jata hai."
