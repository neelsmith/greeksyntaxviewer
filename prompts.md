I want to write a web app as a single HTML file using HTML, Javascript and CSS. The app will allow readers to select annotations on the syntax of Greek texts, and visualize the data in various ways. We'll develop it gradually. First I want to build a UI for loading and organizing the data to visualize. 

Begin by letting the user choose a local file. To load the dataL, I want to use the `cex.js` library. Please include it like this:


```<script src="https://cdn.jsdelivr.net/gh/neelsmith/cex-lib/cex.js"></script>```

Then we'll use its `loadFromFile` function with one parameter, the user-selected file. This will return a `Promise<CEXParser>`. When we have a parser instance, 
we'll use the `getDelimitedData` function three times to collect data about annotated sentences. We'll get annotation on sentences by calling `getDelimitedData("sentences")`, annotatoins on *verbal units* with `getDelimitedData("verbal_units")` and annotations on *tokens* with `getDelimitedData("tokens")` . Here's an example of how you could get the annotations on sentences:

```
const parser = new CEXParser();
parser.loadFromFile(filename)
    .then(p => {
        console.log('CEX data loaded from file!');
        console.log(p.getDelimitedData("sentences"));
    })
    .catch(error => console.error('Failed to load from file:', error));

```


`getDelimitedData` will return a string.

In the result for sentences, each line represents a delimited-text record for a sentence. Each sentence record has three pipe-delimited columns, `sentence`, `sequence` and `connector`. Use the values of the `sentence` column to create a menu allowing the user to select a sentence identifier. Display the user's selection.

In the verbal units data, each line is a record for 1 verbal unit with 5 pipe-delimited columns: `vuid`, `syntactic_type`, `semantic_type`, `depth` and `sentence`. Find all the verbal units with the `sentence` value matching the user's selection of sentence.

In the tokens data, each line is a record for 1 token with 9 pipe-delimited columns, `urn`, `reference`, `tokentype`, `text`, `verbalunit`, `node1`, `node1relation`, `node2` and `node2relation`. For each verbal unit in this sentence, find all the tokens with a `verbalunit` column matching the verbal unit's `vuid` column. List each verbal unit and how many tokens it contains.

---

Great! Now we're going to develop a series of displays for the selected tokens. Make sure they are sorted by the value of numeric `reference` column. Create a single string by joing the `text` value of each token, separated by a space.

---

OK! Now let's format that as follows: 1) no need to display the selected sentence ID since the menu is visible: please remove the section labelled "Selected Sentence ID". 2) Remove the label "Reconstructed Sentence Text:" and remove the gray background. Remove the italic highlighting of the sentence. Display the sentence text against a white ground, and color each token according to its verbal unit. Select a random pastelle color for each verbal unit and use it as a light background for each token in that unit.

---
Great. Now let's modify the disply of verbal units. Move it above the highlighted text display. List each verbal unit on one line as follows: the syntactic type, highlighted in the same way that tokens of that verbal unit are highlighted in the text display, followed unhighlihgted in parentheses by the semantic type of that verbal unit.

---


Super. Let's add an additional further display using the `text` value of each token. We'll need to consider the context as follows: if a token belongs to the same verbal unit as the preceding token, it continues the display on the same line. If it belongs to a different verbal unit, it begins a new line. Line beginnings should be indented according to the depth value of the verbal unit. Level 1 verbal units should be flush left; level 2 units should be indented one level further; etc. Tokens on the same line should be separated by a single white space. Do not use a monospaced font: implement indentation with CSS.

---


Super. Now one further display visualizing the syntax as a Mermaid visualization of a top-down directed graph. Relations among nodes are defined by  columns in the tokens table. `reference` identifies a node; use its `text` column as the label for the node with a given `reference` value.  Use `node1relation` as the label for an edge between `reference` and `node1`; use `node2relation` as the label for an edge between `reference` and `node2`. 

---

Great! I'd like to flip the graph though and make bottom up.

---

Excellent. A couple of tweaks: 1) in the two displays that highlight tokens by verbal unit, let's add decorations for specific values of its `node1relation`. If the value is `unit verb`, add a box around the token; if it is `subject`, add an underline; if it is `direct object`, add both and overline and an underline.

---

The display is good in both the section labelled "Verbal Units" and the "Structured Layout" section, but the Syntax Graph has disappeared! That should not have been changed at all. Could you revert that part of the app so that the Mermaid diagram is restored?

---

Excellent! Here's one further refinement. I would like to put each of the two sections labelled "Structured Layout" and "Syntax Graph  (Mermaid - Bottom to Top") in foldable sections, so that the Verbal Units section would *always* be displayed, but the user could show or hide the "Structured Layout" and "Syntax Graph" sections?

---

Oops. Now the menu to choose sentences is empty so we can't even start!