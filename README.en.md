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
  "questions": [
    {
      "id": 1,
      "question": "Given a = 1 and b = 2, what is a + b?",
      "A": "1",
      "B": "2",
      "C": "3",
      "D": "4",
      "answer": "C",
      "explanation": "Add a = 1 and b = 2, so 1 + 2 = 3. The answer is C."
    }
  ]
}
```

### Field Descriptions

| Field | Required | Description |
| --- | --- | --- |
| `questions` | **Required** | Array of question objects; must not be empty |
| `id` | Optional | If omitted, questions are numbered automatically as 1, 2, 3… |
| `question` | **Required** | The question text |
| `A` / `B` / `C` / `D` | **Required** | The text content of the four options |
| `answer` | **Required** | The correct option: `A`, `B`, `C`, or `D` (case-insensitive) |
| `explanation` | Optional | Explanation text; shows "(No explanation provided)" when omitted |

### Compatibility

The following field aliases are also recognized, so existing quiz banks (including Chinese ones) can be reused as-is:

- `question`: `question`, `title`, `題目`, `题目`
- Options: `A` / `a` / `選項A` (similarly for B, C, D)
- `answer`: `answer`, `答案`
- `explanation`: `explanation`, `解析`, `詳解`, `详解`
- `id` (question number): `id`, `no`, `題號`, `题号`

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

## Tips

- Clicking an option again **deselects** it, returning that question to the unanswered state.
- After shuffling, the question number shown on screen is "the position in this quiz" and is unrelated to the original `id` in the JSON.
- "Restart quiz" does not reload the file, making it ideal for practicing the same quiz bank again.

---

## Changelog

- v1.0 Initial release of the custom quiz site with Chinese/English support
