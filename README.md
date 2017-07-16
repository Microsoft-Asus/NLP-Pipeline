# PipelineNLP
EPFL Semester Project with Professor Dr. Martin Rajman Artificial Intelligence Laboratory Spring 2017 

## DATASETS:
### I. Universal Dependencies 2.0 Dataset:
It consists of 16k sentences in total. You can find this resource along with documentation in http://universaldependencies.org/. You can get both the corpus in its conLL and text format already split into training and testing subsets in all languages for direct download in the following link: https://lindat.mff.cuni.cz/repository/xmlui/bitstream/handle/11234/1-1983/ud-treebanks-v2.0.tgz?sequence=1&isAllowed=y or this link for english only https://github.com/UniversalDependencies/UD_English. 

### II. Sample Treebanks:
You can also get the small sample dataset provided by nltk from http://www.nltk.org/nltk_data/
## I. Lexical Analysis: 
### 1. Creating FSA and Regular Expression Interface:
This implementation has been extracted from http://www.brics.dk/automaton/. Refer to folder src.LexicalAnalysis.FSA for all provided interfaces and methods. Refer to src.LexicalAnalysis.FSA.BasicOperations.java for extensions added to the 
### 2. Extracting Words from Treebank:
This step reads a conLL format file and extracts words from it and builds token FSA based on that: (refer to: src.LexicalAnalysis.Tokenizer.ExtractWordsFromTreebank.java )
 * INPUT: DATASET file in CONLLU format
 * OUTPUT: list of word lemma tags (text + serialized object)  + list of distinct entries (text + serialized object)

### 3. Cleaning wordFSA: 
This step separates pure words or  from common regexes such as numbers, dates, urls to refine their representation in the FSA (refer to: src.LexicalAnalysis.Tokenizer.CleanTokenFSA.java):
 * INPUT: list of distinct words
 * OUTPUT: list of cleaned text distinct words + list of non-text distinct entries

### 4. Creating wordFSA:
This class creates wordFSA with pure word entries: (refer to: src.LexicalAnalysis.Tokenizer.CreateWordFSA.java)
 * INPUT: clean text distinct words
 * OUTPUT: wordFSA
### 5. Creating tokFSA and sepFSA:
This step creates two FSA one is tokFSA (extended from wordFSA created in STEP 3) and sepFSA: (refer to: src.LexicalAnalysis.Tokenizer.CreateFSAs):
 * INPUT: wordFSA
 * OUTPUT: tokFSA + sepFSA
### 6. Tokenizing UDC:
This step tokenizes UDC raw corpus using tokFSA and sepFSA given as inputs and provides as an output the list of tokenized sentences and tokenization charts as determined by EOS specification in the algorithm defined in BasicOperations (refer to src.LexicalAnalysis.Tokenizer.TokenizeUDC.java and for implementation of the algorithm refer to traverseExtendedSolution method in src.BasicOperations)
 * INPUT: raw treebank + tokFSA + sepFSA
 * OUTPUT: tokenized sentences + tokenization charts

### 7. Inspection of Results:
Refer to src.LexicalAnalysis.Tokenizer.ExtractTrueTreebankSentences.java which rebuilds sentences from treebank to be used as a comparison against the tokenized output. You can write to text file using in a readable format the tokenization output charts for visual inspection. Or you can inspecting quantitatively by running src.LexicalAnalysis.Tokenizer.InspectLexicalProcessingResults.java to compute how many sentences have been corrected tokenized.

## II. Morphological Analysis: 
## LIBRARIES:
SFST
