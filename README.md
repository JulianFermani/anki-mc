<!-- omit in toc -->
# anki-mc

Adds multiple choice cards to Anki.

- [Screenshots](#screenshots)
- [Compatibility](#compatibility)
- [Usage](#usage)
  - [Creating / Editing](#creating--editing)
  - [Importing cards from txt/csv](#importing-cards-from-txtcsv)
  - [Reviewing](#reviewing)
  - [Addon Config](#addon-config)
  - [Known Issues](#known-issues)
- [License and Credits](#license-and-credits)

## Screenshots

|                  Single Choice                  |                   Multiple Choice                   |              Kprim              |
| :---------------------------------------------: | :-------------------------------------------------: | :-----------------------------: |
| ![Single Choice](screenshots/single_choice.png) | ![Multiple Choice](screenshots/multiple_choice.png) | ![Kprim](screenshots/kprim.png) |

## Compatibility

Anki 2.1.55 or higher is required for the most recent version of this add-on to work.
For Anki 2.1.44 to 2.1.54, you can use v2.8.0 (or lower) of the add-on.

Cards created with this add-on can be reviewed with all Computer and mobile apps and on AnkiWeb.

## Usage

### Creating / Editing

The note type is automatically added the first time you start Anki after installing the add-on.

When creating cards, write a "1" for correct choices or a "0" for incorrect choices in the "Answers" field.
The question type can be selected with the field "QType".
It can be either 0 (Kprim), 1 (Multiple Choice) or 2 (Single Choice).
The [Screenshots](#screenshots) section shows how the question types look.
These values in the "Answer" field must be separated by a single space.
This fork supports up to 10 answer choices per note, using fields `Q_1` through `Q_10`.
The order and number of values in the "Answer" field must correspond with the choices `Q_1` to `Q_10`.
If you don't need all the choices, just leave the remaining "Q_" fields blank and only enter as many values as you need in the "Answers" field.
This fork uses the note type `Multiple Choice Extended` to avoid conflicting with the original add-on's `AllInOne (kprim, mc, sc)` note type.
Keyboard shortcuts support answer rows 1 to 10; use `Alt+0` for the tenth row.

![Editing](screenshots/edit.png)

### Importing cards from txt/csv

You can import cards from a comma-separated text file by choosing the `Multiple Choice Extended` note type in Anki's import dialog.
Use this exact column order so Anki can assign fields automatically without manual mapping:

```csv
Question,Title,QType,Q_1,Q_2,Q_3,Q_4,Q_5,Q_6,Q_7,Q_8,Q_9,Q_10,Answers,Sources,Extra 1
Which options are correct?,Simple example,1,Option 1,Option 2,Option 3,Option 4,Option 5,Option 6,Option 7,Option 8,Option 9,Option 10,1 0 1 0 0 1 0 0 1 0,,
Is this statement true?,True or false,2,True,False,,,,,,,,,1 0,,
```

For multiple choice (`QType` = `1`), `Answers` can contain several `1` values.
For single choice (`QType` = `2`), use one `1` and mark the rest as `0`.
For Kprim (`QType` = `0`), each answer is evaluated as yes/no.

A ready-to-use example is included at [`docs/import_example_10_answers.csv`](docs/import_example_10_answers.csv).

Column meaning:

- `Question`: the question text.
- `Title`: an optional title. Leave it empty if you do not need it.
- `QType`: use `1` for multiple choice, `2` for single choice, or `0` for Kprim.
- `Q_1` to `Q_10`: possible answers. Leave unused answer columns empty.
- `Answers`: one number per used answer, separated by spaces. Use `1` for correct and `0` for incorrect.
- `Sources`: optional sources. Leave it empty if you do not need it.
- `Extra 1`: optional extra explanation. Leave it empty if you do not need it.

Simple rule: if you wrote 4 possible answers, `Answers` must have 4 numbers. If you wrote 10 possible answers, `Answers` must have 10 numbers.

Example with 4 possible answers:

```csv
Question,Title,QType,Q_1,Q_2,Q_3,Q_4,Q_5,Q_6,Q_7,Q_8,Q_9,Q_10,Answers,Sources,Extra 1
Which planet is known as the Red Planet?,Planets,2,Earth,Mars,Jupiter,Venus,,,,,,,0 1 0 0,,
```

Example with 10 possible answers:

```csv
Question,Title,QType,Q_1,Q_2,Q_3,Q_4,Q_5,Q_6,Q_7,Q_8,Q_9,Q_10,Answers,Sources,Extra 1
Which numbers are even?,Even numbers,1,1,2,3,4,5,6,7,8,9,10,0 1 0 1 0 1 0 1 0 1,,
```

Prompt you can give to an AI to generate cards:

```text
Create Anki multiple-choice cards in CSV format for the note type "Multiple Choice Extended".
Use this exact header:
Question,Title,QType,Q_1,Q_2,Q_3,Q_4,Q_5,Q_6,Q_7,Q_8,Q_9,Q_10,Answers,Sources,Extra 1

Rules:
- Put the question in Question.
- Put a short optional title in Title, or leave Title empty.
- Put QType before the answer options.
- Put each possible answer in Q_1, Q_2, Q_3, etc.
- Use up to 10 possible answers.
- Leave unused Q columns empty.
- In Answers, write one number per used answer, separated by spaces.
- Use 1 for correct answers and 0 for incorrect answers.
- Use QType 1 when there can be multiple correct answers.
- Use QType 2 when there is only one correct answer.
- Leave Sources and Extra 1 empty unless useful.
- Keep the exact column order so Anki imports without manual field mapping.
- Return only CSV, no explanations.
```

### Reviewing

Select the correct and incorrect choices accordingly and click "Show Answer".
The add-on will automatically style your choices based on whether you answered correctly or not.

### Addon Config

If you want to change the way your answers are styled (e.g. color green what you should have chosen instead of what you have chosen correctly) you can use the addon's config to switch between different styles:
![Addon Config Window](screenshots/addon_config.png)
(Tools -> Addons -> "Select the multiple choice addon" -> Config)


### Known Issues
- [I don't understand the colors](https://github.com/zjosua/anki-mc/pull/90)
  - Use the [addon's config](#addon-config) with `ALTERNATE_COLORING`
- [Turn off shuffling/randomization of answers](https://github.com/zjosua/anki-mc/issues/87#issuecomment-1259818989)
  - Possible by duplicating the note type `Multiple Choice Extended` and replacing `qanda = shuffle(qanda);` with `// qanda = shuffle(qanda);`.
- More than 5 answer options
  - This fork raises the default supported choices from 5 to 10 (`Q_1` to `Q_10`).

## License and Credits

*Multiple Choice for Anki* is *Copyright © 2023 [3ter](https://github.com/3ter) and [zjosua](https://github.com/zjosua)*

It is licensed under the AGPLv3.
For more information refer to the [LICENSE](https://github.com/zjosua/anki-mc/blob/master/LICENSE) file.

A bunch of code in this add-on is based on the Anki add-ons [Image Occlusion Enhanced](https://github.com/glutanimate/image-occlusion-enhanced) and [Cloze Overlapper](https://github.com/glutanimate/cloze-overlapper) by Glutanimate.
[Click here to support Glutanimate's work](https://glutanimate.com/support-my-work/).

Persistence is achieved using the code from [Simon Lammer's anki-persistence](https://github.com/SimonLammer/anki-persistence).
Great work Simon!

[Hax](https://github.com/Schlauer-Hax) merged my Multiple Choice card template with Simon Lammer's persistence code.
He also reworked my card templates into one single all-in-one template.
Thanks a lot!

Simon's and Hax's work made the multiple choice cards compatible with all platforms.

Volker Umpfenbach contributed a change that allows to customize how the questions and answers are colorized.
He also provided the code to calculate and display the percentage of correctly answered items per question.

This add-on uses the [packaging](https://packaging.pypa.io/en/latest/) library.
