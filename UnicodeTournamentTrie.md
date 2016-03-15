# Introduction #

The UnicodeTournamentTrie combines [Trounament Trees](http://en.wikipedia.org/wiki/Selection_algorithm#Tournament_Algorithm) with [Tries](http://en.wikipedia.org/wiki/Trie) to extract the best suggestions for the user input.


# Details #

First of all, the places and streets are ranked: Places are ranked by place type and population. Streets are simply ranked by length. Then, a prefix trie with path compression is build for each place containing all street names. Next, the trie is converted into a tournament tree. Finally, a trie / tournament tree is built containing all place names.

Each trie is stored in a highly efficient manner: Edges point directly to the target node's position in the file, edge labels are stored in UTF-8 and node information is stored with the edges rather than with the nodes.

To extract suggestions the plugin now searches for the prefix node matching the user input. Within the sub-tree of this node a tournament tree selection algorithm is run to extract the _k_ top ranked results.