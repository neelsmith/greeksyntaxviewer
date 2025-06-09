# Greek syntax viewer, version `1.1.0`.


> *A vibe-coded single-page web app to visualize syntactic annotations created with this [`greeksyntaxannotator`](https://github.com/neelsmith/greeksyntaxannotator)*.


`syntaxviewer.html` is an app for visualizing syntactically annotated Greek texts. 

There is a user's guide in [`guide.md`](./guide.md)

## Main features


- load annotations created with [`greeksyntaxannotator`](https://github.com/neelsmith/greeksyntaxannotator) from a local text file
- text display is color code by verbal construction words belong to 
- highlighting identifies subject, verb and object (if any) in each verbal unit
- optionally display text indented to show subordination
- optionally visualize a diagram of syntactic relations as a directed graph 

## Caveats

The web app and the user's guide were both written entirely by gemini-2.5-pro. The code passes some sanity tests, but I have not even looked at the javascript. When I encountered errors, I let gemini fix them. Use the code as you like, but be aware that I have no idea what it does or how it works.


### Auditing the build

The file `chat.txt` has the complete chat session that was used to build this app.