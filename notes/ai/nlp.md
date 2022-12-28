# Natural Language Processing

- Sentence -> Tokenize (break sentence into words or document into sentences)
- Tokens are then stemmed or lemmatized
    - stemming- chop off common prefixes and suffixes (common one is the PorterStemmer)
    - lemmitization- using linguistic knowledge to find the roots of words (requires dictionaries for the language to provide morphological analysis)
- In [linguistics](https://en.wikipedia.org/wiki/Linguistics), **morphology** ([/mɔːrˈfɒlədʒi/](https://en.wikipedia.org/wiki/Help:IPA/English)[[1\]](https://en.wikipedia.org/wiki/Morphology_(linguistics)#cite_note-1)) is the study of words, how they are formed, and their relationship to other words in the same language.[[2\]](https://en.wikipedia.org/wiki/Morphology_(linguistics)#cite_note-2)[[3\]](https://en.wikipedia.org/wiki/Morphology_(linguistics)#cite_note-3) It analyzes the structure of words and parts of words such as [stems](https://en.wikipedia.org/wiki/Stem_(linguistics)), [root words](https://en.wikipedia.org/wiki/Root_(linguistics)), [prefixes](https://en.wikipedia.org/wiki/Prefix), and [suffixes](https://en.wikipedia.org/wiki/Suffix). 

## Text Feature Extraction

- [sklearn user guide](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction)
- Want numerical vectors to represent the text we are working with so we can throw it into common ML/DL algorithms
- A corpus of documents can be represented by a matrix with one row per document and one column per token (e.g. word) occurring in the corpus.
    - very sparse representation (>99% zeros) so use `scipy.sparse`
-  **vectorization** the general process of turning a collection of text documents into numerical feature vectors
    - **Bag of Words**- tokenization, counting and normalization
        - aka “Bag of n-grams” representation
        - no info on words position in the document stored in this representation