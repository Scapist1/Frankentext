# Frankentext

1. replace_non_printable_chars_with_space()
Iterates through every character in the book text.
Replaces non-printable characters (like \xEF, tabs, etc.) with a space ' '.
Purpose: ensures tokenization is consistent and clean.
2. tokenize_and_fill_succs(delimiters, book)
Splits the book string into tokens (words) using delimiters:
" \n\r"
For each token:
Registers it using token_id(token) (adds it to tokens[] if new).
Links it to the previous token with append_to_succs(prev, token).
Updates prev = token.
Purpose: builds the word list (tokens[]) and successor map (succs[][]) used for sentence generation.
3. srand(time(nullptr))
Seeds the random number generator with the current time.
Purpose: ensures different random outputs each time the program runs.
4. Generate a Question Sentence
Loop until a sentence ends with ?:
Call generate_sentence(sentence, sizeof sentence).
Inside this function:
Choose a random starting word that begins with a capital letter (random_token_id_that_starts_a_sentence()).
Append random successors one by one.
Stop if:
The sentence would exceed the buffer, or
A token ends with ., ?, or ! (token_ends_a_sentence()).
Check if last_char(sentence) is '?'; repeat if not.
Print the final question sentence.
5. Generate an Exclamation Sentence
Loop until a sentence ends with !:
Same process as above, reusing generate_sentence().
Continue until last_char(sentence) is '!'.
Print the final exclamation sentence.
