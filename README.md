Download Link: https://assignmentchef.com/product/solved-cs2223-homework-4
<br>
<h1>Q1. Word Ladders: Breadth First Search Exercise</h1>

A word ladder is a word game invented by Lewis Carroll. A word ladder puzzle begins with two words of the same length. To solve the puzzle, you must find a sequence of other words to link the two, in which two adjacent words in successive steps differ by one letter.

For example, given the words COLD and WARM, the following is a sample word ladder:

COLD à CO<u>R</u>D à C<u>A</u>RD à <u>W</u>ARD à WAR<u>M</u>

Note how each successive word differs by exactly one letter from the prior word. While the sequence of words can be quite long, the goal of this question is to come up with the shortest path given a dictionary of valid English words (such as found in <strong>words.english.txt</strong> which you can find in the repository).

Here are the assumptions you can make:

<ol>

 <li>All words in the word ladder are just four letters long. Use an AVL&lt;String&gt; tree to store all these words.</li>

 <li>You are to use a table SeparateChainingHashST&lt;String,Integer&gt; <em>table</em> to store the mapping from a four-letter word to an integer, representing that word’s vertex in the undirected graph.</li>

 <li>You are to use a table SeparateChainingHashST&lt;Integer,String&gt; <em>reverse</em> to store the reverse mapping from the integer vertex id to the four-letter word.</li>

</ol>

Copy algs.hw4.WordLadder into your USERID.hw4 package and modify it to solve this problem. Here are some hints:

<ol>

 <li>Use an AVL&lt;String&gt; tree (as implemented in hw4.AVL) to store all four-letter English words. You can load up the “words.english.txt” file and add all four-letter words to this</li>

</ol>

AVL tree. Because it is an AVL tree, it will self-balance as words are inserted in ascending order.

<ol>

 <li>As each word is added to the AVL tree, add an entry into <em>table</em> and <em>reverse</em>.</li>

 <li>Next, create a graph, G, with the same number of vertices as there are words in <em>table</em>.</li>

 <li>Now for the final trick, add an undirected edge (u, v) to this graph G if two words (W<sub>u</sub> and W<sub>v</sub>) differ by just a single letter.</li>

</ol>

A final hint: how to process all pairs of words in the AVL tree? Consider the following:

String min = avl.min(); <strong>for</strong> (String w1: avl.keys()) { <strong>  for</strong> (String w2: avl.keys(min, w1)) {   // will do one more check than necessary…     …

} }

This will allow you to process all pairs of words (W<sub>u</sub> and W<sub>v</sub>). Note that you need to write logic to determine if two Strings differ by just a single letter.

<h1>Q2. Finding the Longest Word Ladder Using This Dictionary</h1>

Given the available English words, can you find the longest Word Ladder that exists in this collection?

<strong>Property NonRepeating:</strong>  You must avoid the obvious ways to have a longest word ladder, that is, repeating a pair of words over and over (like card à cord à card à cord). Thus each of the words in the word ladder must be distinct.

<strong>Property MinimalDistance</strong>: Second, given the starting and ending words – S and E – in your candidate longest word ladder, there must be no shorter word ladder that exists between these two terminal words. For example, the word ladder “card à cord à word à ward” consists of four words, but there exists a shorter word ladder from card (which is S) and ward (which is E), namely “card à ward.”

Here is my one-sentence definition. “The Longest Word Ladder is formed from two words S and E such that (a) there is no shorter word ladder between S and E; and (b) no other <strong>NonRepeating</strong> and <strong>MinimalDistance </strong> word ladder exists between two different words, A and B, which is longer.”

It turns out that there is one involving 17 English words (which means there are sixteen transformations):

abri,absi,assi,asse,arse,erse,else,elle,ells,alls,alps,amps,imps,impy,immy,is my,isms

Can you find it programmatically?

Copy algs.hw4.LongestWordLadder into your USERID.hw4 package and modify it to solve this problem. You will still load up an AVL tree containing the keys (as in Question 1). Now you should consider using multiple requests to DijkstraUndirectedSP on the graph from different source vertices.

Note: as an alternative, you could consider constructing a directed graph and use the FloydWarshall implementation (edu.princeton.cs.algs4.FloydWarshall) to compute the two words that require the most steps in a word ladder.

Finally, this question is only required to print out the TWO words that are at the end of the word ladder. Once these two words are printed out (together with the number of steps) you only need to run the WordLadder solution you developed in Q1 to show that you have found this word ladder.




<h1>Q3. BONUS question: Word Pyramid [1 pt]</h1>

A word pyramid is a word game. A word pyramid puzzle begins with a word of N letters. To solve the puzzle, you must find a sequence of other words, of decreasing size in length, until you reach a word with just a single letter. To produce the next word in the sequence, remove a letter and form a new word from the remaining letters

For example, given the starting word, RELAPSE, the following is a sample word pyramid:

RELAPSE à PEARLS à SPEAR à PEAS à SEA à AS à A

Note how each successive word differs by exactly one letter from the prior word (and is an anagram of the remaining letters). Each of the subsequent words must be a valid word (such as found in <strong>words.english.txt</strong> which you can find in the repository).

Here are the assumptions you can make:

<ol>

 <li>The length of the initial word will be seven characters or less.</li>

 <li>You are to use a table SeparateChainingHashST&lt;String, Integer&gt; <em>table</em> to store the mapping from a word to an integer, representing that word’s vertex in the undirected graph.</li>

 <li>You are to use a table SeparateChainingHashST&lt;String, Integer&gt; <em>reverse</em> to store the reverse mapping from the integer vertex id to its associated word.</li>

</ol>

This is a bonus question, so you are on your own. Feel free to create a new class based on the Q1 Word Ladder class. Here is my sample output from a run:

Enter word to start from (all in lower case): relapse relapse serape spear spar spa pa a


