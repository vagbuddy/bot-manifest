# Rules for Writing Code Comments (Anti-AI Slop Edition)

You write comments that explain **why** code exists, not **what** the code does. Imagine your reader is a tired, cynical senior developer who can read the syntax perfectly but wants to know the hidden context, constraints, or business logic.

## 🎯 Core Principles

1.  **Code explains the "What"; Comments explain the "Why":** Never rewrite the code in plain English. If the code is `if (status === 'active')`, do not write `// Check if status is active`.
2.  **Context & Constraints over Syntax:** Explain why a specific approach, hack, or magic number was used. 
3.  **Ruthless Brevity:** Use fragments. Drop pronouns (*I, we, you, this*), articles (*the, a, an*), and polite fillers where possible.
4.  **No Hand-Waving:** Avoid words that hide a lack of understanding (e.g., "properly", "handles", "safely"). Be precise.

---

## 🚫 AI Comment Slop Detection (Blacklist)

Do NOT use these phrases, structures, or filler words. If any of these appear in your comments, the comment is rejected.

### 1. Banned Explanatory Fillers
*   `This function/method/class...` (We can see it's a function)
*   `This variable stores...` (We can see it's a variable)
*   `Is used to...` / `Responsible for...`
*   `In order to...` (Just say "To")
*   `Make sure to...` / `Please note that...`

### 2. Banned "Smart-Sounding" Vagueness
*   `...properly cleans up resources` -> *State exactly what it deletes or closes.*
*   `...handles edge cases` -> *Name the specific edge case (e.g., "if connection drops").*
*   `...ensures safety/security` -> *State the specific vulnerability or crash being blocked.*
*   `...for better performance` -> *State the benchmark or reason (e.g., "avoids O(N^2) loop").*

### 3. Banned AI Formatting Habits
*   **The "Docstring Echo":** Repeating the exact parameter names and types in a comment right below the type definition.
*   **The "Captain Obvious" Block:** Adding 3 lines of comments to a 1-line self-explanatory helper method.

---

## 🛠️ Concrete Examples

### Example 1: Refusing to State the Obvious
❌ **AI Slop:**
```javascript
// Initialize the user counter to zero
let userCounter = 0;
```
👉 **Fix (Delete completely):** The code is self-documenting. No comment needed.

### Example 2: Explaining the "Why" (The Hidden Constraint)
❌ **AI Slop:**
```typescript
// Set timeout to 400 milliseconds for the animation to properly complete
setTimeout(initializeUI, 400);
```
✅ **Anti-Slop:**
```typescript
// 400ms matches CSS transition in layout.css; avoids race condition on slower devices
setTimeout(initializeUI, 400);
```

### Example 3: Documenting a Hack or Workaround
❌ **AI Slop:**
```python
# We need to use a try-except block here to safely catch potential API errors 
# and ensure the application does not crash unexpectedly.
try:
    fetch_legacy_data()
except Exception as e:
    logger.error(e)
```
✅ **Anti-Slop:**
```python
# Legacy API randomly drops connection without headers. Catch prevents crash.
try:
    fetch_legacy_data()
except Exception as e:
    logger.error(e)
```

---

## 🤖 AI Execution Workflow

When writing or editing comments, you must pass through this 2-step mental filter:

1.  **Drafting:** Write the comment focusing only on the technical "why", the business reason, or the edge case.
2.  **The "Slop Trim":** Read your draft. Delete any articles (*the, a*), delete introductory words, and make it as punchy as possible. If it states what the next line of code does, **delete the entire comment.**
