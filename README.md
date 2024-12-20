This project utilizes Hunalign and the Gemini API for aligning English and French texts from novels, focusing on segmentation, character position tracking, and pronoun alignment using various resources including the Dialogism project.

## Getting Started

### Prerequisites

#### Hunalign
Download Hunalign from the following repository:
- [Hunalign GitHub Repository](https://github.com/danielvarga/hunalign/tree/master)

#### Gemini API
Obtain an API key for Gemini:
- [Gemini API Documentation](https://ai.google.dev/gemini-api/docs?gad_source=1&gclid=CjwKCAiAyJS7BhBiEiwAyS9uNa0OtIC8fnaA4kKfXhp2CRFvDh5ut0PaU3um-bFrl0XYbeEFnX_pphoCXZAQAvD_BwE)

> **Note:** This project used three different API keys for testing. You will need to replace the API key in your configurations.

#### Dialogism Project
Fetch English novel texts from the Dialogism project:
- [Dialogism Speaker Attribution Project](https://github.com/Priya22/speaker-attribution-acl2023)

### Directory Structure
Ensure the following structure in your local setup:

```
hunalign-1.1/
│
├── hunalign/ (All Hunalign-related files)
├── 1_prepare_text_nlp.ipynb
├── 2_find_characters.ipynb
├── res/
│   ├── data/
│   ├── data_test/
│   ├── accuracy/
│   └── punk/
```

#### Folder Descriptions
- `data`: Contains book folders with original English and French versions, a translation dictionary, and sample French texts for training.
- `data_test`: For testing alignment accuracy on smaller text segments.
- `res`: Stores CSV files from Dialogism, segmented texts by Hunalign, and necessary dictionaries for Hunalign.
- `accuracy`: Includes output from Hunalign and alignment checks.
- `punk`: Contains pickles for training space tokenizers in various languages.

### Key Files and Their Usage (all except mentioned_used.csv created by code)
- `mentioned_used.csv`: Entity list used from each novel.
- `alignments_with_char_positions.csv`: Adjusted text by Hunalign/Gemini with character positions from the original text.
- `may_need_realign.csv`: Alignments that may need realignment due to index discrepancies.
- `pronoun_alignment_with...`: There are three files associated with pronoun alignment:
  - `pronoun_alignment_without_gemini.csv`: Transferred entities using only project-specific algorithms.
  - `pronoun_alignment_with_gemini.csv`: Transferred entities using both project-specific algorithms and Gemini API.
  - `pronoun_alignment_with_only_gemini.csv`: (Test case only) Transferred entities using only the Gemini API, utilized for statistical analysis. 
  - These files encompass all data from the original `mentioned_used.csv` for English, including the French alternatives found, as well as the indices and phrases themselves.
- `with_gemini_correction`: Files that hold the English and French entities with their indices and additional details similar to those in `mentioned_used.csv`. They include a "check" column to indicate whether Gemini assessed the entity transfers as correct. This set includes:
  - `with_gemini_correction.csv`: Used for regular checks.
  - `with_gemini_only_correction_test.csv`: Used specifically to compare the outcomes of hybrid approaches versus Gemini-only scenarios.
- `updated_alignments`: Final alignment table.
- `realigned_need_to_transfer_annotations`: This table, like many others, ensures that Gemini's work is accurately recorded after each update, considering the limited number of free API calls available. It lists phrases that required realignment after being initially aligned by Gemini in groups. The `id` column holds the previous IDs from the `updated_alignments` that were already aligned but needed to be realigned as they served as a buffer between groups of unaligned text. This mechanism prevents the duplication of entries.


## Execution Instructions
1. **Prepare Text and call Hunalign**:
   - Start with `1prepare_text_nlp.ipynb`, following the setup instructions within.
   - run Hunalign
       - Detailed instructions for running Hunalign commands post-text preparation are included at the end of the `1prepare_text_nlp.ipynb` notebook.
2. **Find Characters**:
   - Continue with `2find_characters.ipynb`. This script may require multiple runs due to API token limitations. Change the Gemini API key if needed to handle rate limits.


