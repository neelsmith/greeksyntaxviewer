
## Greek Syntax Viewer - User Guide

`syntaxviewer.html` allows you to load annotated Greek text data and explore its syntactic structure through various visualizations.

**1. Loading Your Data:**

*   **Choose File:** Click the "Choose a CEX file" button.
*   **Select File:** In the dialog that appears, navigate to and select your local `.cex` (CEX format) file containing the annotated Greek text.
    *   *Note:* The CEX file must contain data blocks named `sentences`, `verbal_units`, and `tokens` for all features to work correctly. The app will provide warning messages if any of these are missing.

**2. Selecting a Sentence:**

*   Once the file is successfully loaded, the "Select Sentence" dropdown menu will become active and populate with sentence identifiers from your data.
*   Click the dropdown and choose a sentence you wish to analyze.

**3. Understanding the Displays (once a sentence is selected):**

*   **Verbal Units:**
    *   This section (always visible) lists each verbal unit found within the selected sentence.
    *   Each entry shows:
        *   **Syntactic Type:** (e.g., "Finite Verb", "Participle") highlighted with a unique color. This color corresponds to the highlighting of tokens belonging to this verbal unit in the text displays below.
        *   **(Semantic Type):** (e.g., "Action", "State") in parentheses.
        *   **ID & Token Count:** The internal ID of the verbal unit and the number of tokens it contains.

*   **Key (Collapsible):**
    *   Click on the "Key" heading to expand or collapse this section.
    *   This legend explains the visual decorations applied to tokens in the text displays:
        *   <span class="key-example key-example-box" style="border: 1.5px solid #333;">Verb</span> : Indicates a token that is the primary verb of its unit (often where `node1relation` is 'unit verb').
        *   <span class="key-example key-example-subject" style="text-decoration: underline; text-decoration-color: #333; text-decoration-thickness: 1.5px; text-underline-offset: 3px;">Subject</span> : Indicates a token identified as the subject of a verb.
        *   <span class="key-example key-example-direct-object" style="text-decoration: overline underline; text-decoration-color: #333; text-decoration-thickness: 1.5px; text-underline-offset: 3px;">Object</span> : Indicates a token identified as the direct object of a verb.

*   **Continuous Text Display:**
    *   This section (always visible) shows the full text of the selected sentence.
    *   Each token is:
        *   **Colored:** The background color of each token matches the color of its verbal unit shown in the "Verbal Units" list.
        *   **Decorated:** Tokens may have boxes, underlines, or overlines+underlines according to the "Key" based on their syntactic role (specifically, their `node1relation` value).

*   **Text indented by level of subordination (Collapsible):**
    *   Click on the heading to expand or collapse this section.
    *   This display presents the sentence's tokens grouped by their verbal unit.
    *   Tokens belonging to the same verbal unit appear on the same line.
    *   When a new verbal unit begins, it starts on a new line.
    *   Lines are indented from the left margin based on the `depth` value of their verbal unit, visually representing levels of syntactic subordination.
    *   Tokens are colored and decorated as in the continuous text display.

*   **Syntax Graph (Collapsible):**
    *   Click on the heading to expand or collapse this section.
    *   This shows a graphical representation of the syntactic relationships between tokens in the sentence.
    *   It's a bottom-to-top directed graph:
        *   **Nodes (Boxes):** Represent individual tokens, labeled with their text.
        *   **Edges (Arrows):** Connect tokens, showing relationships. The label on an arrow (e.g., "subject", "adjunct") indicates the type of relationship from the source token to the target token, based on the `node1relation` or `node2relation` values in your data.

**Troubleshooting:**

*   **Empty Sentence Menu:** Ensure your CEX file contains a `sentences` block with valid data.
*   **Missing Features/Warnings:** If "verbal\_units" or "tokens" blocks are missing or malformed in your CEX file, some displays might be empty or show limited information. Check the status messages below the file input.
*   **Graph Errors:** If the graph doesn't render, there might be an issue with the token relationship data or an internal Mermaid error. Check the browser's developer console for more details.

