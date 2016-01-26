# LexicalChains

### Steps to Run
1.	Open lexicalChains.py
2.	Place the text file titled “nlp.txt” in the current working directory
3.	Run lexicalChains.py
4.	Type input filename (use “nlp” or create own test file) in the console when prompted


### Program description

lexicalChains.py reads a text file as input, identifies and print all the lexical chains.

First, the text file is read and all the nouns are extracted and stored in a list. 
Each noun is then passed as a parameter to the function add_word(word)
add_word checks for all the chains that have been created so far, for all the synsets of the parameter word, for all the senses of each word in each chain,
and compares the synsets using:

•	Path similarity: 
synset1.path_similarity(synset2): Return a score denoting how similar two word senses are, based on the shortest path that connects the senses in the is-a (hypernym/hypnoym) taxonomy. The score is in the range 0 to 1. By default, there is now a fake root node added to verbs so for cases where previously a path could not be found---and None was returned---it should return a value. The old behavior can be achieved by setting simulate_root to be False. A score of 1 represents identity i.e. comparing a sense with itself will return 1.

•	Wu-Palmer Similarity:
Return a score denoting how similar two word senses are, based on the depth of the two senses in the taxonomy and that of their Least Common Subsumer (most specific ancestor node). Note that at this time the scores given do _not_ always agree with those given by Pedersen's Perl implementation of Wordnet Similarity. The LCS does not necessarily feature in the shortest path connecting the two senses, as it is by definition the common ancestor deepest in the taxonomy, not closest to the two senses. Typically, however, it will so feature. Where multiple candidates for the LCS exist, that whose shortest path to the root node is the longest will be selected. Where the LCS has multiple paths to the root, the longer path is used for the purposes of the calculation.

•	Jiang-Conrath Similarity: 
Return a score denoting how similar two word senses are, based on the Information Content (IC) of the Least Common Subsumer (most specific ancestor node) and that of the two input Synsets. The relationship is given by the equation 1 / (IC(s1) + IC(s2) - 2 * IC(lcs)).


The threshold values for each of these similarity functions is set as:
Wupthreshold = 0.6

jcnTreshold = 0.09

pathTeshold = 0.1 



### Data Structures: 

The program uses a class called Chain with attribute word and senses and methods to set and get word and senses.
A dictionary is used to store the count of each word, where the key is the word, value is the count.
A list of array of Chain objects stores all the lexical chains in the text file.
