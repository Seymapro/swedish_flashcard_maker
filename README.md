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

5.  **Merging Classified Chunks:** A script reads all the individual classified chunk files from the `classified_chunks` directory, concatenates them using `pandas`, removes potential duplicates, and saves the result as a single, comprehensive CSV file (e.g., `classified_wordlist_all.csv`).

6.  **Generating Prompts:** A script to generate prompt using Gemini.

7. **Generating Images From the Wordlist CSV File**: This Python script uses Imagen3 the prompts that Gemini created.  

## Prerequisites

* Python 3.x
* `pandas` library (`pip install pandas`)
* `google-generativeai` library (`pip install google-generativeai`)
* A Google AI API Key (obtainable from [Google AI Studio](https://aistudio.google.com/))
* Your initial Swedish-English vocabulary list (must be converted to CSV format).
* The Python scripts associated with this project (for cleaning, chunking, classifying, merging).
* Anki (to use the final generated deck).

## Installation

1.  **Clone the repository (if applicable):**
    ```bash
    git clone <your-repository-url>
    cd <your-repository-directory>
    ```
    (Ensure the Python scripts are present in the directory).
2.  **Install dependencies:**
    ```bash
    pip install pandas google-generativeai
    ```
3.  **Set up your API Key:**
    * **Recommended:** Set an environment variable named `GEMINI_API_KEY`.
        * Linux/macOS: `export GEMINI_API_KEY='your_api_key_here'`
        * Windows (cmd): `set GEMINI_API_KEY=your_api_key_here`
        * Windows (PowerShell): `$env:GEMINI_API_KEY='your_api_key_here'`
    * *Alternatively:* Configure the API key directly within the classification script (ensure not to commit sensitive keys to version control).

## Usage

1.  Place your initial Swedish-English wordlist file (converted to CSV format) in the project directory.
2.  Run the **Data Cleaning** script, ensuring input/output filenames match your needs.
3.  Run the **Chunking** script, using the cleaned CSV as input.
4.  Ensure your `GEMINI_API_KEY` is accessible (e.g., via environment variable).
5.  Run the **AI Word Type Classification** script. It will process files from the `chunks` directory (or as configured) and save results.
6.  Run the **Merging Classified Chunks** script to combine the classified files into the final CSV output.
7.  **(Next Steps - Manual/External)** Use the final generated CSV file as input for further processing:
    * Generate audio files (e.g., using Text-to-Speech services).
    * Generate images (e.g., using image generation APIs).
    * Format the data and import it into Anki using its import functionality.

## Contributing

Contributions, issues, and feature requests are welcome! Please feel free to open an issue or submit a pull request.

## License

[Specify Your License Here - e.g., MIT, GPL, Apache 2.0]

## Acknowledgements

* The initial wordlist was sourced from [studium.uu.se](https://studium.uu.se).
* This project utilizes the [Google Gemini API](https://ai.google.dev/).


