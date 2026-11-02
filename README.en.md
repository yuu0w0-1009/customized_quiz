# Custom Quiz Bank v1.0
[中文](README.md) ｜ **English**

A purely front-end static website for "custom quiz banks"

**Zero dependencies, no installation, no backend** — just upload a JSON quiz bank file and start the quiz immediately

---
## Main Features
1. Customizable quiz bank
2. Shuffle questions
3. Answer progress tracking
4. Result statistics
5. Wrong answer review

## Quiz Bank JSON Format

### Structure

```json
{
  "題目數": 1,
  "題目": [
    {
      "題號": 1,
      "題目": "Given a = 1 and b = 2, what is a + b?",
      "A": "1",
      "B": "2",
      "C": "3",
      "D": "4",
      "答案": "C",
      "詳解": "Add a = 1 and b = 2: 1 + 2 = 3, so the answer is C."
    }
  ]
}
```

### Field Descriptions

| Field | Required | Description |
| --- | --- | --- |
| `題目數` | Optional | For reference only; the actual total is based on the length of the `題目` array |
| `題目` | **Required** | Array of question objects; must not be empty |
| `題號` | Optional | If omitted, questions are numbered automatically as 1, 2, 3… |
| `題目` | **Required** | The question text |
| `A` / `B` / `C` / `D` | **Required** | The text content of the four options |
| `答案` | **Required** | The correct option: `A`, `B`, `C`, or `D` (case-insensitive) |
| `詳解` | Optional | Explanation text; shows "（無提供詳解）" when omitted |

### Compatibility

The following field aliases are also recognized, so existing quiz banks can be reused as-is:

- `題目` (question): `題目`, `题目`, `question`, `title`
- Options: `A` / `a` / `選項A` (similarly for B, C, D)
- `答案` (answer): `答案`, `answer`
- `詳解` (explanation): `詳解`, `详解`, `解析`, `explanation`
- `題號` (number): `題號`, `题号`, `id`, `no`

If the file contains a BOM (`\uFEFF`) character, it is removed automatically before parsing. Line breaks in the explanation can be written as `\n` and are preserved when displayed.

---

## Usage Flow

```
File loading page
  └─ Select / drag a .json file → validation passes → total question count shown → start quiz
       └─ Quiz page (one question at a time, with a shuffle option)
            └─ Submit (a confirmation dialog appears if any question is unanswered)
                 └─ Results page (accuracy rate, wrong answer list)
                      ├─ View all explanations → review question by question → finish → back to results
                      ├─ Restart quiz (keeps the quiz bank, answer again)
                      └─ Start over (clears all state)
```

---

## Project Structure

```
.
├── index.html      # Main program, contains all HTML / CSS / JavaScript
├── example.json    # Sample quiz bank (3 questions, same as the site's "Download sample JSON")
└── README.md
```

---

## Tips

- Clicking an option again **deselects** it, returning that question to the unanswered state.
- After shuffling, the question number shown on screen is "the position in this quiz" and is unrelated to the original `題號` in the JSON.
- "Restart quiz" does not reload the file, making it ideal for practicing the same quiz bank again.

---
