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