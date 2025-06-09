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
In the result for sentences, each line represents a delimited-text record for a sentence. Each sentence record has three pipe-delimited columns, `sentence`, `sequence` and `connector`. Use the values of the `sentence` column to create a list of identifiers for sentences in the text.

In the verbal units data, each line is a record for 1 verbal unit with 5 pipe-delimited columns: `vuid`, `syntactic_type`, `semantic_type`, `depth` and `sentence`.

In the tokens data, each line is a record for 1 token with 9 pipe-delimited columns, `urn`, `reference`, `tokentype`, `text`, `verbalunit`, `node1`, `node1relation`, `node2` and `node2relation`. For each verbal unit in this sentence, find all the tokens with a `verbalunit` column matching the verbal unit's `vuid` column. 


The first part of the UI to build is a menu allowing the user to select a sentence identifier. Filter the list of sentences to include only those sentences which appear as a value in the `sentence` column of the verbal units data, and create a menu of these. Display the user's selection.

When the user chooses a sentence, find all the verbal units with the `sentence` value matching the user's selection of sentence. For each verbal unit, choose a pastel color that is easily distinguished from all other selected colors.
Create a list of the verbal units displaying them as follows highlight the value of `syntactic_type` using the unique color for that verbal unit, then in parentheses give the `semantic_type`, then show how many tokens it contains.

---

Great! Tiny tweak: in the list of verbal units' syntactic, keep the background color as it is but make the text black.

---

Another tiny tweak: do not include the header line of the table in forming the menu. The label `sentenced` should not appear in the menu.

---


Beautiful. Now we're going to develop a series of displays for the selected tokens. Make sure they are sorted by the value of numeric `reference` column. Create a single string by joing the `text` value of each token, separated by a space.
Display the sentence text against a white ground, and color each token according to its verbal unit.


---

Let's futher decorate this display of tokens for specific values of its `node1relation`. If the value is `unit verb`, add a box around the token; if it is `subject`, add an underline; if it is `direct object` or `predicate`, add both and overline and an underline.

---

Super. Let's add an additional further display. We'll use the `text` value of each token, and will create an indented display considering the context as follows: if a token belongs to the same verbal unit as the preceding token, it continues the display on the same line. If it belongs to a different verbal unit, it begins a new line. Line beginnings should be indented according to the depth value of the verbal unit. Level 1 verbal units should be flush left; level 2 units should be indented one level further; etc. Tokens on the same line should be separated by a single white space. Do not use a monospaced font: implement indentation with CSS. Please color and highlight each token as in the preceding display of the continuous sentence.

---

Now one further display visualizing the syntax as a Mermaid visualization of a bottom-up directed graph. Relations among nodes are defined by  columns in the tokens table. `reference` identifies a node; use its `text` column as the label for the node with a given `reference` value.  Use `node1relation` as the label for an edge between `reference` and `node1`; use `node2relation` as the label for an edge between `reference` and `node2`. 

---

Gorgeous! That's all the key functionality! Now tweaking the display:  I would like to put each of the two sections labelled "Sentence Text (Structured by Verbal Unit Depth):" and "Syntax Graph (Mermaid): in foldable sections, so that the Verbal Units section would *always* be displayed, but the user could show or hide the "Structured Layout" and "Syntax Graph" sections. Immediately above the "Sentence Text (Continuous):" I'd like to add a further collapsible section, titled "Key". Its header should be smaller than the other sections. The conents of the seciton should list three pieces of information, namely:

- *boxes* == verb forms
- *underscore* == subject of verb
- *underscore + overline* == direct object

---

Perfect. Let's make the "Key" section foldable, too.

---

I'd like to give the user the option of displaying ther mermaid syntax diagram either left to right or top to bottom. Could you implement that?

--

Excellent! Let's make the default option "Top to Bottom"
