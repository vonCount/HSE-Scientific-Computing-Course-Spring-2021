Data representation I

Exercise: Pretend we use a naïve floating-point format with 5bit mantissa and 3bit exponent (base-2). What is the smallest possible positive number representable? What is the largest positive number representable? The first bit of each is used for sign:

	[±****][±**]
	 ^^^^^  ^^^--- exponent
	   |---------- mantissa
One of the many perils of working with floating-point numbers: recall that the fraction 1/3 has an infinitely long decimal expansion, while 1/10 has a finite expansion:

	1/10 = 0.1
	1/3  = 0.333…
In binary, we have a similar problem: powers of 2 have finite expansions, while 1/10 has an infinite expansion:

	1/2  = 0.1₂
	1/10 = 1/16 + 1/32 + 1/256 + ⋯
	     = 0.00011001… ₂
Since our processors use binary floating point, we have to truncate (cut off) this representation, resulting in an imperfect approximation of 1/10.

Exercise: use python to check this:

from decimal import Decimal

print(repr(Decimal(0.1)))
should result in

Decimal('0.1000000000000000055511151231257827021181583404541015625')
Exercise: what is the best approximation of 0.01?

Read the Python floating point tutorial for more information on how this can apply to python.


Linked lists

Linked lists are data structures where each item is allocated individually, and is stored with a next reference (usually the memory address) of the next item. If next is null (a special value to indicate no address, typically the zero address), the end of the list has been reached.

---------------       ---------------       ---------------
| x[0] | next |--->---| x[1] | next |--->---| x[2] | NULL | 
---------------       ---------------       ---------------
Changing the size of a linked list is very cheap: to add, you find the two items you want to insert between, and update the "next" pointers (in the correct order!):

---------------       ---------------       ---------------
| x[0] | next |--->-- | x[1] | next |--->---| x[2] | NULL | 
---------------       ---------------       ---------------
                      /
           --------------
           |  y  | next |
	   --------------


---------------       ---------------       ---------------
| x[0] | next |       | x[1] | next |--->---| x[2] | NULL | 
---------------       ---------------       ---------------
            \         /
           --------------
           |  y  | next |
	   --------------
To delete, you update the "next" pointer of the previous item to match the "next" pointer of the deleted item.

Exercise: use diagrams like the above to explain how to delete an item from a linked list.

Linked lists can be upgraded in various ways; for example, a doubly-linked-list has next and previous pointers, so it can be traversed in either direction.

The operation of adding an item to a linked list is called "insertion".

Stacks, queues

Stacks are a data structure in which items are visualised as being in a "stack": the only item accessible is the last item added; the only way to access earlier items is by removing the items added afterwards. The operation of adding to top of a stack is called "pushing", while removing from the top is called "popping". (The last item in the stack is called the "top".)

Queues are the opposite: the only item accessible is the first item added; to access items added later, the first item must be removed. Adding to the head of the queue is called "enqueuing", and removing "dequeuing". (The first item of the queue is called the "head".)

Trees

Trees are the most obvious way to construct a hierarchy: a tree starts with an item (typically called the "root") and pointers to a number of other subordinate items. The subordinates are called "children"; each item is allowed to have children. In this way we can refer to parents, descendents, ancestors.

Here we have the root node R, with children A and B. R is the parent of A and B. The tree has leaves X, Y, Z, and W; they have R as a grandparent, and A, B, R as ancestors.

           R
	  / \
	 A   B--
        / \   \ \
       X   Y   Z W
There are many different types of trees: a tree is binary if every node has at most two children. If the items can be ordered (for example, they are numbers), then a binary search tree is a binary tree such that the value of a node is greater than every descendent to the left, and less than every descendent to the right. A binary search tree is balanced if for every node, the sizes of the left and right subtrees differ by at most one.

Exercise: assemble the numbers 1-10 into binary search trees which are (a) maximally unbalanced to the left, (b) balanced, (c) one step from balanced.

Graphs

A graph is a non-hierarchical data structure admitting many-to-many relationships. The fundamental data of a graph is an unordered collection of items ("nodes" or "vertices"), and for each node a list of connections to other nodes ("edges").

Examples:

          ---          C 
         /   \       /   \
        A --- B     A --- B  E         A - B
         \   /       \
          ---          D 
A directed graph is a collection of vertices together with a list of ordered connections to other graphs:

          -<-          C 
         ↙   ↖       ↗   ↘
        A ->- B     A ->- B  E         A -> B
         ↖   ↙       ↘
          -<-          D 
A path in a graph or directed graph is a list of edges to follow. (If the graph is directed, the path must respect the edge directions.) The first node in the path is called the source or the start or the tail; the last is called the sink or the end or the head.

A graph is called connected if every node has a path to every other node. (Whether the graph is directed or not is irrelevant for this.)

A cycle is a path which starts and end are the same. A graph which has no cycles is called acyclic.

Exercise: assemble a directed acyclic graph with the numbers 1-12 by strict divisibility: an edge from A to B if B/A is prime. There are no directed cycles, but some nodes do have multiple paths to them. (These form cycles if you ignore the direction.) Which ones? Explain how to decide if a number will have multiple paths to it.

Every directed acyclic graph has at least one maximum spanning tree: a directed tree (i.e., arrows always point away from the root) inside the graph which touches every node.

Exercise: Identify several maximal spanning trees in the divisibility graph from the previous exercise.

Exercise: model acquaintance using a graph (vertices are people, an edge between A and B means A knows B). Model it with a directed graph. How are these different?


Hashing

Suppose you have transferred a large data file; how do you check there were no errors? A first strategy is to check the size: if they have the files have different sizes, an error definitely occurred.

A more sophisticated strategy is to create a checksum: split the data into small pieces, interpreted as numbers, and add them all together. If the answers are the same, either the errors added to 0 (via overflow), or else the pieces are all the same.

Exercise: this doesn't mean the file was transferred correctly; why not?

The topic of error detection codes is rich, and won't be covered here (though it is very important for the theoretical study of language!).

A more sophisticated strategy is to use a hash function. A hash function is a way to associate a number (the "hash") to data, in a way that it is extremely unlikely that you will be able to find two blocks of data with the same hash (called a "collision"). The process of applying the hash function is called "hashing."

Some popular hash algorithms are:

md5
sha1
sha2 / sha3
blake2
Some hash algorithms are used for cryptography, and need to have certain mathematics justifying important properties (e.g., unlikelihood of finding collisions, lack of correlation between data and its hash, and others). For our purposes, we want our hash to not have collisions, but cryptographic strength is not important.

You can experiment with hashes on Linux or other UNIX-like systems. Typically hashes are displayed not as decimal numbers, but rather as hexadecimal, using digits 0-9a-f.

$ echo hi > testfile; echo hi2 > testfile2

$ md5sum testfile testfile2
764efa883dda1e11db47671c4a3bbd9e  testfile
4da1c6449a2a34a338e56d6718838016  testfile2

$ sha1sum testfile testfile2
55ca6286e3e4f4fba5d0448333fa99fc5a404a73  testfile
906faceaf874dd64e81de0048f36f4bab0f1f171  testfile2

$ sha512sum testfile testfile2 # sha2, hash size is 512bit
d78abb0542736865f94704521609c230dac03a2f369d043ac212d6933b91410e06399e37f9c5cc88436a31737330c1c8eccb2c2f9f374d62f716432a32d50fac
testfile
d1fde846964c462fe3686eb0c2bed0ab1c66feb77bd06a8f6aefdca90c04036b8c8bdd8ee65567ea2f4d30714f4343d0151a13b9937473d526f3cda5d5413023
testfile2

$ b2sum testfile testfile2 # blake2
7ea59e7a000ec003846b6607dfd5f9217b681dc1a81b0789b464c3995105d93083f7f0a86fca01a1bed27e9f9303ae58d01746e3b20443480bea56198e65bfc5
testfile
768d17d444de521eb82f9c45cf0d6384c87f18ea67e164c7a832e24ab47483be0c006fc8ab806694e670f4df306468c5f30f6a987f7f8ba02c011ba641db3a7b
testfile2

Notice that hashes are completely changed even though the file contents are nearly the same.

Exercise: do the same for files with "cat" and "cat2" instead of "hi" and "hi2"

Symmetric cryptography

You might know cryptography in the sense of symmetric ciphers: there is a secret SEC. To encrypt a message M, called the cleartext, you apply a mathematical operation enc(SEC, M). The result is the ciphertext X.

Anyone who knows the same secret SEC can apply a mathematical operation dec(SEC, X) to recreate the message, that is,

dec(SEC, X) = dec(SEC, enc(SEC, M)) = M
Exercise: implement the Caesar cipher in python, which advances each letter of 'M' by 'SEC = n': enc(1, "a") = "b", etc.

Asymmetric cryptography

Asymmetric cryptography works differently: there is a pair of related keys (numbers), for now call them A and B. Just like with symmetric cryptography, there is a mathematical operation RSA(key, x). The keys A and B have a special relationship: if a message is encrypted with A, it is decrypted by B, and vice-versa:

RSA(A, RSA(B, M)) = M
RSA(B, RSA(A, M)) = M
Without B, RSA(A, x) cannot be decrypted, even with A.

The first system for constructing such A, B, and RSA is called the [Rivest-Shamir-Adelman algorithm], after the three authors. Now there are many such systems, not all of which can properly be called RSA.

Read and attempt to follow along with the PGP tutorial.

