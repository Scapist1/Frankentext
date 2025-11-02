# 📘 Markov Sentence Generator

This program reads the text from `pg84.txt`, tokenizes it, builds a successor map between words (Markov chain), and generates random sentences that resemble the source text.  
It keeps generating until it finds both a *question* sentence (`?`) and an *exclamation* sentence (`!`).

---

## 🧩 Program Overview

The program performs these main steps in `main()`:

### 1. `replace_non_printable_chars_with_space()`
- Iterates through every character in the book text.  
- Replaces non-printable characters (like `\xEF`, tabs, etc.) with a space `' '`.  
- **Purpose:** ensures tokenization is consistent and clean.

---

### 2. `tokenize_and_fill_succs(delimiters, book)`
- Splits the `book` string into **tokens** (words) using delimiters: `" \n\r"`.  
- For each token:
  - Registers it using `token_id(token)` (adds it to `tokens[]` if new).  
  - Links it to the previous token with `append_to_succs(prev, token)`.  
  - Updates `prev = token`.  
- **Purpose:** builds the word list (`tokens[]`) and successor map (`succs[][]`) used for sentence generation.

---

### 3. `srand(time(nullptr))`
- Seeds the random number generator with the current time.  
- **Purpose:** ensures different random outputs each time the program runs.

---

### 4. Generate a Question Sentence
- Loop until a sentence ends with `?`:
  1. Call `generate_sentence(sentence, sizeof sentence)`.  
  2. Inside this function:
     - Choose a random starting word that begins with a capital letter (`random_token_id_that_starts_a_sentence()`).  
     - Append random successors one by one.  
     - Stop if:
       - The sentence would exceed the buffer, or  
       - A token ends with `.`, `?`, or `!` (`token_ends_a_sentence()`).  
  3. Check if `last_char(sentence)` is `'?'`; repeat if not.  
- Print the final question sentence.

---

### 5. Generate an Exclamation Sentence
- Loop until a sentence ends with `!`:
  - Same process as above, reusing `generate_sentence()`.  
  - Continue until `last_char(sentence)` is `'!'`.  
- Print the final exclamation sentence.

---

## ⚙️ Helper Functions Summary

| Function | Description |
|-----------|--------------|
| `token_id(token)` | Returns index of token in `tokens[]`, inserting if not found. |
| `append_to_succs(token, succ)` | Adds `succ` to the list of successors of `token`. |
| `last_char(str)` | Returns the last character of a string. |
| `token_ends_a_sentence(token)` | Returns `true` if the token ends with `.`, `?`, or `!`. |
| `random_token_id_that_starts_a_sentence()` | Picks a random token whose first letter is uppercase. |

---

## 🧠 Summary

- **Input:** Text from `pg84.txt` (embedded).  
- **Process:** Tokenize → Build successor map → Generate random sentences.  
- **Output:** Two sentences — one ending with `?` and one with `!`.

---

## 💻 How to Compile and Run
