![anan](https://img.shields.io/badge/gay-sex-blue?link=-)
![anan](https://img.shields.io/badge/ku%C5%9Fsiken-31-yellow?link=-)

# Swedish Anki Flashcard Generator 

This project provides a workflow and scripts to transform a Swedish-English vocabulary list into a structured CSV file suitable for creating enhanced Anki flashcards. The process leverages AI (Google Gemini) to automatically classify word types (noun, verb, phrase), laying the groundwork for generating Anki decks potentially enriched with AI-generated audio pronunciations and illustrative images (Note: image/audio generation steps are not included in these specific scripts but are the intended final goal).

## Features

* Parses Swedish-English vocabulary lists (initially from .docx, converted to CSV).
* Cleans raw vocabulary data using a dedicated script.
* Chunks large wordlists into smaller files using a script to work within API limits.
* Utilizes Google Gemini AI via a script to determine the grammatical type (noun, verb, phrase) for each entry.
* Merges the classified data back into a single, structured CSV file using a script.
* Outputs a clean CSV file ready for further processing into an Anki deck.

## Methodology / Workflow

The process involves several steps, executed by distinct Python scripts, to prepare the vocabulary data:

1.  **Initial Data Extraction:** The vocabulary list was originally sourced from a `.docx` file (found on studium.uu.se). This needs to be converted into a two-column CSV file (`Swedish`, `English`) before processing.

2.  **Data Cleaning:** A Python script reads the initial CSV, removes artifacts (like `►` symbols) or formatting inconsistencies using `pandas` and `regex`, and saves a cleaned version of the CSV.

3.  **Chunking:** To handle potentially large vocabulary lists and stay within API request limits for AI processing, a script divides the cleaned list into a specified number of smaller CSV files (chunks), typically saved in a `chunks` subdirectory.

4.  **AI Word Type Classification:** Another script iterates through each chunk file. It sends the content of the chunk to the Google Gemini API with instructions to identify whether each line contains a noun, verb, or phrase. The script then saves the AI's response, which should include the original data plus a new 'Type' column, into a corresponding file in a `classified_chunks` directory. This script requires a configured Google AI API key.

5.  **Merging Classified Chunks:** A script reads all the individual classified chunk files from the `classified_chunks` directory, concatenates them using `pandas`, removes potential duplicates, and saves the result as a single, comprehensive CSV file (e.g., `classified_wordlist_all.csv`). The script then turns the CSV file into JSON since it's more convenient to name the variables in that way.

6.  **Generating Prompts:** A script to generate prompt using Gemini.

7. **Generating Images From the Wordlist CSV File**: This Python script uses Imagen3 the prompts that Gemini created. The 'Type' column is also important here since some words are heteronym.

8. **Generating Sounds From the Wordlist CSV File:**  This Python script uses Elevenlabs API to pronounce Swedish words.

9. **Creating and Importing .apgk File to Anki:** The script takes Swedish and English words from the JSON file and images and sounds from the files i previously generated. I used genanki repository to do so.

## Prerequisites

* Python 3.x
* `pandas` library (`pip install pandas`)
* `google-generativeai` library (`pip install google-generativeai`)
* A Google AI API Key (obtainable from [Google AI Studio](https://aistudio.google.com/))
* Your initial Swedish-English vocabulary list (must be converted to CSV format).
* The Python scripts associated with this project (for cleaning, chunking, classifying, merging).
* Anki (to use the final generated deck).
* [Genanki repository](https://github.com/kerrickstaley/genanki)

## Installation

The reop is not ready for installation yet.


## Contributing

Contributions, issues, and feature requests are welcome! Please feel free to open an issue or submit a pull request.

## License

MIT license

## Acknowledgements

The initial wordlist was sourced from studium.uu.se.
This project utilizes the Google Gemini API.

* The initial wordlist was sourced from [studium.uu.se](https://studium.uu.se).
* This project utilizes the [Google Gemini API](https://ai.google.dev/).
* This project utilizes [genanki](https://github.com/kerrickstaley/genanki)


