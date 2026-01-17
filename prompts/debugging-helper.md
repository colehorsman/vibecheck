# Debugging Helper Prompt

Use this to systematically debug issues.

---

## The Prompt

```
I'm getting this error:

[PASTE ERROR MESSAGE]

Here's the relevant code:

[PASTE CODE]

Context:
- What I was trying to do: [DESCRIPTION]
- When it happens: [TRIGGER - e.g., on form submit, on page load]
- What I've tried: [ATTEMPTS]

Help me:
1. Understand what's causing this error
2. Fix it with specific code changes
3. Prevent similar issues in the future
```

---

## Quick Debug

```
Error: [PASTE ERROR]

Code: [PASTE RELEVANT CODE]

What's wrong and how do I fix it?
```

---

## "It's Not Working" Debug

```
This code isn't working as expected:

[PASTE CODE]

Expected behavior: [WHAT SHOULD HAPPEN]
Actual behavior: [WHAT'S HAPPENING]

Help me figure out why.
```

---

## API Not Responding

```
My API call isn't working:

Code:
[PASTE FETCH/AXIOS CODE]

Expected: [EXPECTED RESPONSE]
Getting: [ACTUAL RESPONSE OR ERROR]

Network tab shows: [STATUS CODE, RESPONSE]

What's wrong?
```

---

## Database Query Issues

```
This database query isn't returning expected results:

Query:
[PASTE QUERY]

Expected: [EXPECTED RESULTS]
Getting: [ACTUAL RESULTS]

Table schema:
[PASTE SCHEMA OR DESCRIBE STRUCTURE]

What's wrong with my query?
```

---

## Component Not Rendering

```
This React component isn't rendering correctly:

[PASTE COMPONENT CODE]

Expected: [WHAT SHOULD APPEAR]
Actual: [WHAT'S APPEARING OR NOT APPEARING]

Console errors: [ANY ERRORS]

What's the issue?
```

---

## Build/Deploy Error

```
My build is failing with this error:

[PASTE BUILD ERROR]

package.json:
[PASTE RELEVANT PARTS]

Config files:
[PASTE RELEVANT CONFIG]

How do I fix this?
```

---

## Systematic Debug Template

```
Help me debug this issue systematically:

## The Problem
[DESCRIBE THE ISSUE]

## Error Message
[PASTE EXACT ERROR]

## Code
[PASTE RELEVANT CODE]

## Environment
- Node version: [VERSION]
- Framework: [FRAMEWORK + VERSION]
- OS: [OS]

## Steps to Reproduce
1. [STEP 1]
2. [STEP 2]
3. [STEP 3]

## What I've Tried
- [ATTEMPT 1]
- [ATTEMPT 2]

## Questions
1. What's causing this?
2. How do I fix it?
3. How do I prevent it in the future?
```

---

## Tips

- Include the EXACT error message
- Show the relevant code, not the entire file
- Mention what you've already tried
- Include environment details for build issues
- Check the browser console AND terminal
