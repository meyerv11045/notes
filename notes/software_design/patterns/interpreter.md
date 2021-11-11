# Interpreter Pattern

## Intent
Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the languages 

## Applicability
- When the grammar is simple and relatively stable (e.g. don't use for a programming language like C++)
- Efficiency is not a critical concern 

## Structure
graphical representation of pattern using modified UML notation

## Participants
participatnig classes/objects and their responsibilities

## Collaborations
How participants cooperate to carry out their responsibilities

## Consequences
- (+) Simple grammars are easy to change and extend
    - All rules are represented by distinct classes in an orderly manner
- (+) Adding another rule adds another class
- (-) Complex grammars are hard to yield and maintain 
    - More interdependent rules yield more interdependent classes

## Implementation
- Express the language rules, one per class
- Alternations, repetitions, or sequences expressed as nonterminal expressions
- Literal translations expressed as terminal expressions
- Create interpret method to lead the context through the interpretation classes

## Sample Code

## Known Uses

## Related Patterns