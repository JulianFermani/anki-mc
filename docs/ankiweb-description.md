# Multiple Choice Extended

An Anki add-on for creating interactive multiple-choice cards.

This fork extends the original multiple choice add-on by supporting up to 10 possible answers per card.

## Features

- Multiple choice cards
- Single choice cards
- Kprim-style cards
- Up to 10 answer options
- Works with imported CSV/TXT cards
- Uses the note type `Multiple Choice Extended` to avoid conflicts with the original add-on

## Import Format

When importing from CSV/TXT, use this field order:

```csv
Question,Title,QType,Q_1,Q_2,Q_3,Q_4,Q_5,Q_6,Q_7,Q_8,Q_9,Q_10,Answers,Sources,Extra 1
```

`QType` values:

- `0` = Kprim
- `1` = Multiple Choice
- `2` = Single Choice

In the `Answers` field, use:

- `1` for correct answers
- `0` for incorrect answers

Example:

```csv
Which numbers are even?,Numbers,1,1,2,3,4,5,6,7,8,9,10,0 1 0 1 0 1 0 1 0 1,,
```

## Credits

Based on the original Multiple Choice for Anki add-on by zjosua, 3ter, and contributors.

This fork adds extended answer support and import documentation.
