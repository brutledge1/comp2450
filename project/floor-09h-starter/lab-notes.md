1. A transcript of the demo above (your own hero name).



> selftest balance

&#x20; balanceFactor: empty==0, bushy==0, left-leaning==1: OK

&#x20; isBalanced: bushy {5,3,8,2,4,7,9} balanced (true): OK

&#x20; degenerate: sorted stick {1..6} is NOT balanced (height 5): OK

&#x20; rotate: rotateRootLeft on {1,2,3} -> root 2, height 1, order kept: OK

&#x20; balanceRoot: right- and left-heavy sticks both rebalance (order kept): OK

&#x20; all phases OK

> balance

&#x20; McCown's catalogue: 15 names, height 6, root balance factor -3 ΓÇö NOT balanced (lopsided).

> benchmark balance



\-- Same sorted input: your plain BST vs std::set (1000 iterations per cell) --

&#x20; N=     10  plain BST: height=     9  find=    0.684 us    std::set: find=   0.492 us

&#x20; N=    100  plain BST: height=    99  find=    8.051 us    std::set: find=   1.363 us

&#x20; N=   1000  plain BST: height=   999  find=   70.874 us    std::set: find=   1.614 us



Same data, same order. Inserted in sorted order, your plain BST

degenerated into a stick of height N-1 ΓÇö lookup is back to O(n).

std::set saw the identical input and stayed shallow: it is a

balanced tree (a red-black tree) that rotates on every insert to

hold its height near log2 N. You do not hand-write that balancing ΓÇö

you reach for std::set / std::map. That is the next floor, the

Hall of Names.



> quit

McCown notes your departure. "You leave in order."



2\. The lean, by hand. On paper, insert 1, 2, 3, 4, 5, 6, 7 into an empty BST in that order and draw the stick. Write the balance factor at the root (1) and at the middle node (4), counting an empty side as −1. Then draw the balanced tree on the same seven values (root 4). One sentence: same values, same rule — what is different, and why does it change how many nodes find has to look at?



In the first scenario the balance factor of the root and middle node were -6 and -3 while in the second scenario they were 0 at both the root (4) and (1) nodes. This reduces the amount of nodes needed to search by reducing the overall height of the tree. In the worst case scenarios the first tree would have to check 7 nodes and the second would only check 4. 



3\. A rotation, by hand. Insert 3, 5, 8 in that order: 3 at the top, 5 as its right child, 8 as 5’s right child. Do a left rotation at 3. Draw the result and write the in-order walk before and after. Confirm they match. One sentence: why does “in-order unchanged” mean the result is still a valid BST?



Because the order is unchanged it means the BST adheres to the rule of left being lower values and right being greater values. 



4\. Which rotation? For each unbalanced root, name the rotation rebalanceAt would apply and why: (a) a left-heavy root (balance factor +2); (b) a right-heavy root (−2). Then the case one rotation can’t fix: insert 1, 3, 2 (so 2 is 3’s left child). Do one left rotation at 1 and draw what you get. Is it balanced now? One sentence: what does a real AVL tree do instead? (You do not have to code it.)



For the left-heavy root a right rotation is needed and for a right-heavy root a left rotation is needed. In both of these scenarios the goal is to reduce the heavy side by rotating one of the nodes to its weaker side. One rotation would create an invalid tree because the node 3 would have a right node less than its root. Another rotation is needed to set it right.



5\. The comparison. Run benchmark balance. Paste the table. (Your microseconds will not match the page; the heights will.) In two sentences, in your own words: the plain BST and the std::set saw the identical sorted input — why did one become a stick and the other stay short? What is std::set doing on every insert that your BST is not?



\-- Same sorted input: your plain BST vs std::set (1000 iterations per cell) --

&#x20; N=     10  plain BST: height=     9  find=    1.550 us    std::set: find=   2.619 us

&#x20; N=    100  plain BST: height=    99  find=   10.919 us    std::set: find=   1.284 us

&#x20; N=   1000  plain BST: height=   999  find=   53.255 us    std::set: find=   1.139 us



The plain BST is adding the values without modifying itself. That means if a string of many larger values are inserted it will create a long strand. The set is looking at each of its nodes as a new value is inserted and judging whether it needs to rotate it based on the balance factor.



6\. One-paragraph reflection. You stopped one step short of a self-balancing tree on purpose. Was that the right call? When, if ever, would you write the balancing yourself instead of using std::set/std::map? And: you’ve built five pointer structures and are about to start using one you didn’t write. What do you gain, and what do you give up?



The built in std::set accomplishes the goal of checking if each node needs to be rebalanced and saves a good amount of code for what could have been a less effective process. I imagine what we lose by choosing to use set rather than making our own is the choice of what rules the tree should follow. We've learned about two different types of trees: AVL and the red and black trees. The red and black tree was considered more practical and forgiving with its less strict balance factor requirements but if you want to get the quickest possible path down then the AVL should always accomplish this purpose. I'm not 100 percent sure what kind of balance factor the std::set makes use of, but this lack of control in structure would be one reason to use a self built ADT rather than a provided one. 

