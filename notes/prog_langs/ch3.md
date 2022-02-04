## Ch. 3 Describing Syntax and Semantics

## 3.1 Introduction

- **Syntax**- the *form/structure* of the expressions, statements, and program units
- **Semantics**- the *meaning* of the expressions, statements, and program units 
- Syntax and semantics provide a language's definition
- Semantics should follow from syntax in a well designed programming language
- Language Definition Users:
    - Initial evaluaors (language designers)
    - Implementers (compiler writers)
    - Programmers (language users)

## 3.2 Describing Syntax

- A language is a set of strings of characters from some alphabet 
    - Sentences/Statements are the strigns of a language
- Describing a language with english can lead to many issues (e.g. Fortran)
- **Meta-Language**- a language used to define other languages
- **Grammar**- a meta-lanugage used to define the syntax of a language
- A sentence can be syntactically correct but not semantically correct

### Lexical Analysis

- Lexical specification is usually seperate from syntactic description
    - lexemes include literals, operators, keywords, etc.
    - programs are strings of lexemes
- Converting characters in the source program into lexical units 	
- Lexical analyzer splits source code into tokens
- Token- syntactic category that forms a class of lexemes
    - identifiers (names of vars, methods, classes) , literals, keywords, operators, punctuation
- Lexeme- a sequence of characters that matches the pattern for a token 

### Formal Definition of Languages

- Two ways:
    - Recognizer- reads input strings over the alphabet of the language and decides whether the input strings belong to the language 
      - produces a yes/no answer as to whether the input string is a valid sentence in the language
      - Syntax analysis is a recognizer
    - Generator- generates random valid sentences in a specific language
  
- Neither on their own are useful in learning a language

- Used together they form the basis of computational theory
  
  

## 3.3 Formal Methods of Describing Syntax

- Grammars- used to descirbe the syntax of programming languages

### Context Free Grammars

- Developed by Noam Chomsky (a linguist)
- 4 classes of generative devices or grammars that define 4 classes of languages
    - 2 of them, context-free and regular grammars, were later useful for describing the syntax of programming languages
    - forms of tokens in PLs can be described by regular grammars
    - syntax of whole languages can be described by context-free grammars

### Backus-Naur Form (BNF)

- Invented by John Backus to describe Algol 58
- A natural notation for describing syntax
- Equivalent to context-free grammars
- Metalanguage for PLs
- Grammar consists of:
    - *Start symbol*
    - Finite set of *production rules*
    - Finite set of *terminal symbols*
    - Finite set of *nonterminal symbols*
- Uses abstractions for syntactic structures
    - `<assign> -> <var> = <expression>` is a definition of the assign abstraction where the LHS of the arrow is the abstraction being defined and the RHS of the arrow consists of a mixture of tokens, lexemes, and references to other abstractions 
    - the definition is called a *production rule*
- nonterminal symbols- the abstractions in a BNF description
    - can have 2+ distinct definitions (represent 2+ possible syntactic forms in the language)
    - multiple definitions can be written as a single rule seperated by a `|` meaning logical OR
  - terminal symbols- lexemes and tokens of the rules 
- BNF Description/Grammar- a collection of rules 
- Simple but sufficiently powerful to describe syntax of PLs
    - Lists (utilizes recursion): `<identifier_list> -> identifier | identifier, <identifier_list>` 
    - ordering, nested structures of any depth, operator precedence and associativity 
- Grammar- generative device for defining languages
    - Start with a special nonterminal *start symbol* and then apply a sequence of rules in a *derivation*
      - start symbol is usually `<program>`
- Sentential Form- every string of nonterminal or terminal symbols in a derivation
- Sentence- a sentential form that has only terminal symbols
- Leftmost derivation- leftmost nonterminal in each sentential form is the one that is expanded next
    - derivation could be rightmost or in neither leftmost or rightmost since derivation order has no effect on the generated language
- Most languages are infinite so all sentences in the language cannot be generated in finite time

### Parse Tree

- A hierarchial representation of a derivation
- every internal node is nonterminal symbol
- every leaf node is a terminal symbol

### Ambiguity 

- A grammar is *ambiguous* iff it generates a sentital form that has 2+ distinct parse trees 
    - bad for compilers that need 1 unique parse tree
- If we use parse tree to indicate precedence levels of the operators, we cannot have ambiguity
- operator associativity can also be indicated by a grammar
    - Ex: `<expr> -> <expr> + const | const` indicates left associativity of the `+` operator (left recursion -> left associativity)

#### Dangling Else Ambiguity

- `if (<logic_expr>) if (<logic_expr>) <stmt> else <stmt>` is ambiguous as to which if statement the else belongs to
- Rewrite grammar to restirct what can appear inside a nested if-statement 
- Use `<matched> and` `<unmatched>` abstractions to handle the different types of if-else statements
    - `<stmt> → <matched> | <unmatched>`
    - `<matched> → if (<logic_expr>) <matched> else <matched> |any non-if statement`
    - `<unmatched> → if (<logic_expr>) <stmt> | if (<logic_expr>) <matched> else <unmatched>`