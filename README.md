# Greek syntax viewer


> *A vibe-coded single-page web app to visualize syntactic annotations created with this [`greeksyntaxannotator`](https://github.com/neelsmith/greeksyntaxannotator)*.


`syntaxviewer.html` is an app for visualizing syntactically annotated Greek texts. 

## Status

Version 1.0.0 is an intitial release. Its main features are:

- load annotations created with [`greeksyntaxannotator`](https://github.com/neelsmith/greeksyntaxannotator) from a local text file
- text display is color code by verbal construction words belong to 
- highlighting identifies subject, verb and object (if any) in each verbal unit
- optionally display text indented to show subordination
- optionally visualize a diagram of syntactic relations as a directed graph 

## Caveats

The web app was written entirely by gemini-2.5-pro. The code passes some sanity tests, but I have not even looked at the javascript. When I encountered errors, I let gemini fix them. Use the code as you like, but be aware that I have no idea what it does or how it works.