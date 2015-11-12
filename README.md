# clone-finder
find duplication, compare tree structure data, find code clone (target to refactering).

# Idea

## Concepts

  - adaptive (customizable?)
  - run in terminal
  - use Node.js / MongoDB

## process flow

  - input
    - pass file list (ex. ls, find, ...)
    - read tree structured file (ex. html, xml, plist, ...)
  - tokenize
    - divide text or structured data into token list
    - remove comments, white spaces
    - use lex/yacc ? or use it's grammer?
  - parse
    - generate tree object from token list
    - add property (reserved keyword, constant, variable) to each node
  - compare
    - define comparator
      - isEqual
      - $(diff a b|grep '>'|wc -l) < threshold
    - node <-> leaf, node <-> node, leaf <-> leaf
    - set option
      - compare root to root / compare ancester to descendant
    - generate difference object
      - store in memory / DB (MongoDB?)
      - structure
      ```json
      {
        "aPath": "/foo/bar/buzz",
        "aDepth": 3,
        "bPath": "/hoge/fuga/piyo/bar/buzz",
        "bDepth": 5,
        "score": 230,
        "isSame": true
      }
      ```
  - output
    - collect data
    ```javascript
    store.find({"isSame": true, "aDepth": {"$lt": "bDepth"}}).sort({"score": -1})
    ```
    - print
    ```json
    ["score", "aPath", "bPath"]
    ```
  
# Memo

- clone finder
  http://www.ncbi.nlm.nih.gov/projects/mapview/mvhome/mvclone.cgi?taxid=10090
- Lex/yacc
  http://dinosaur.compilertools.net/
- Fast Tree
  http://meta.microbesonline.org/fasttree/
