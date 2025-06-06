I want to write a web app as a single HTML file using HTML, Javascript and CSS. The app will allow readers to select annotations on the syntax of Greek texts, and visualize the data in various ways. We'll develop it gradually. First I want to build a UI for loading and organizing the data to visualize. 

Begin by letting the user choose a local file. To load the dataL, I want to use the `cex.js` library. Please include it like this:


```<script src="https://cdn.jsdelivr.net/gh/neelsmith/cex-lib/cex.js"></script>```

Then we'll use its `loadFromFile` function with one parameter, the user-selected file. This will return a `Promise<CEXParser>`. When we have a parser instance, we'll use `getDelimitedData("sentences")` to find data about annotated sentences.
```
const parser = new CEXParser();
parser.loadFromFile(filename)
    .then(p => {
        console.log('CEX data loaded from file!');
        console.log(p.getDelimitedData("sentences"));
    })
    .catch(error => console.error('Failed to load from file:', error));

```



`getDelimitedData` will return a string with each line representing a delimited-text record for a sentence. Each record has three pipe-delimited columns, `sentence`, `sequence` and `connector`. Use the values of the `sentence` column to create a menu allowing the user to select a sentence identifier. Display the user's selection.

---

Excellent. Now we want to load two further datasets annotating *verbal units* and *tokens* within sentences. We'll load them the way we loaded the sentences data: use `getDelimitedData("verbal_units")` and `getDelimitedData("tokens")`, respectively, to load these data sets.

The verbal units data is a single string with each line containing the record for 1 verbal unit in 5 pipe-delimited columns: `vuid`, `syntactic_type`, `semantic_type`, `depth` and `sentence`. Find all the verbal units with the `sentence` value matching the user's selection of sentence, and list this.

