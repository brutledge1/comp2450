1. A transcript of the demo above (your own hero name; recall at least three creatures, one of them absent).



**> selftest bst**

&#x20; **empty BST<int>: empty() \&\& size==0 \&\& height==0: OK**

&#x20; **insert: root==5 and size==7 over the sample: OK**

&#x20; **contains: 7 and 2 present, 6 and 404 absent: OK**

&#x20; **inOrder == {2,3,4,5,7,8,9} (ascending): OK**

&#x20; **degenerate: sorted inserts give height==5, not balanced: OK**

&#x20; **deep copy: mutating the original leaves the copy unchanged: OK**

&#x20; **remove: leaf(2), one-child(3), two-children(5) all correct: OK**

&#x20; **all phases OK**

**> catalogue**

**Bone Spider   HP 6   ATK 2   weakness: fire**

**Cave Troll   HP 28   ATK 7   weakness: fire**

**Cinder Bat   HP 4   ATK 1   weakness: water**

**Frostmaw   HP 22   ATK 6   weakness: fire**

**Goblin   HP 8   ATK 2   weakness: fire**

**Ironclaw Bear   HP 24   ATK 5   weakness: slashing**

**Lich   HP 35   ATK 6   weakness: holy**

**Marsh Lurker   HP 18   ATK 3   weakness: fire**

**Necrothrall   HP 16   ATK 4   weakness: light**

**Ratking   HP 9   ATK 2   weakness: fire**

**Shadow Hound   HP 12   ATK 4   weakness: light**

**Skeleton   HP 10   ATK 3   weakness: blunt**

**Stone Sentinel   HP 30   ATK 5   weakness: blunt**

**Wisp   HP 3   ATK 1   weakness: holy**

**Wraith   HP 14   ATK 4   weakness: holy**

&#x20; **(15 creatures, alphabetical; tree height 6)**

**> recall Stone Sentinel**

**Stone Sentinel   HP 30   ATK 5   weakness: blunt**

&#x20; **(recalled from the tree)**

**> recall Wisp**

**Wisp   HP 3   ATK 1   weakness: holy**

&#x20; **(recalled from the tree)**

**> recall Marsh Lurker**

**Marsh Lurker   HP 18   ATK 3   weakness: fire**

&#x20; **(recalled from the tree)**

**> recall No Name**

&#x20; **'No Name' is not in McCown's catalogue.**

**> forget Goblin**

&#x20; **McCown strikes 'Goblin' from the tree. (14 remain.)**

**> benchmark bst**



**-- Bestiary: linear scan vs BST lookup (1000 iterations per cell) --**

&#x20; **N=    100  query=last    linear=     4.298 us  BST=     0.431 us  (tree height 13)**

&#x20; **N=    100  query=absent  linear=     2.866 us  BST=     0.504 us  (tree height 13)**

&#x20; **N=   1000  query=last    linear=    22.226 us  BST=     0.620 us  (tree height 22)**

&#x20; **N=   1000  query=absent  linear=    14.019 us  BST=     0.601 us  (tree height 22)**

&#x20; **N=  10000  query=last    linear=   198.577 us  BST=     0.730 us  (tree height 30)**

&#x20; **N=  10000  query=absent  linear=   141.366 us  BST=     0.667 us  (tree height 30)**

&#x20; **N= 100000  query=last    linear=  2020.914 us  BST=     0.559 us  (tree height 40)**

&#x20; **N= 100000  query=absent  linear=  1644.342 us  BST=     0.529 us  (tree height 40)**



**Linear scan grows with N; BST lookup grows with log N ΓÇö the same**

**win binary search gave you on Floor 1, but now the structure STAYS**

**searchable as you insert and remove, with no re-sort step.**

**One catch: this tree was built from SHUFFLED data. Insert the**

**monsters already sorted and the BST degenerates into a stick**

**(height \~N), and lookup drops right back to linear ΓÇö the problem**

**the next floor's self-balancing tree exists to solve.**



**> quit**

**McCown notes your departure. "You leave in order."**



2\. The invariant, by hand. On paper, insert 8, 3, 10, 1, 6, 14, 4, 7, 13 into an empty BST, one at a time, drawing the tree after each. Then trace find(7): write down which way you go at each node, how many nodes you look at, and how many you never look at. One sentence: how does the number you looked at compare to the tree’s height?



**8 -> Left -> 3 -> Right -> 6 -> Right -> 7. Looked at four nodes ignored 5. The number of nodes we looked at matched the tree's height. In the worst case scenario it seems that the most steps taken is bound by the height of the tree.** 



3\. In-order is sorted. Write out the in-order traversal of your tree from step 2. Confirm it’s ascending. In two sentences: why does “left, node, right” produce sorted order — what does the invariant guarantee about everything in the left subtree?



**1, 3, 4, 5, 6, 7, 10, 13, 14. The left, node, right sequence ensures that any left most value (which will be smaller than the root) is counted first, then the root itself, then any values to the right of the root node (which should be greater). This means that even with some values being greater than the roots of the subtree, a parent root that is to the right of the subtree root is guaranteed to be of greater value than any of the subtree's nodes.** 



4\. The three removals. From your tree, remove 4, then 10, then 8 (the root). Draw the tree after each and name which case fired: leaf, one child, or two children. For the root: which node moved up, and why does that value keep the tree in order, being bigger than everything on its left and smaller than everything else on its right?



**The 4 node was removed without any replacement as there was no child nodes, the 14 node moved to replace the 10 node, and the 8 node was replaced by the 13 node. The reason the 8 node could be replaced by the 13 node was because it was the smallest value to the right of the parent node. We could follow this by going once to the right then continuing to follow left until you could no longer go down. Alternatively you could have also used 7 by going down one to the left then all the way right, making it the biggest of the smaller than values.** 



5\. The degeneracy experiment. Run benchmark bst. Paste the table. Then, in two sentences, explain the closing note: if you had inserted the monsters in alphabetical order instead of shuffled, what would the tree’s height have been, and what would have happened to recall’s speed? (You are describing the problem Floor 9½ exists to solve.)



**-- Bestiary: linear scan vs BST lookup (1000 iterations per cell) --**

&#x20; **N=    100  query=last    linear=     5.117 us  BST=     0.377 us  (tree height 13)**

&#x20; **N=    100  query=absent  linear=     1.246 us  BST=     0.238 us  (tree height 13)**

&#x20; **N=   1000  query=last    linear=    22.085 us  BST=     0.667 us  (tree height 22)**

&#x20; **N=   1000  query=absent  linear=    14.441 us  BST=     0.606 us  (tree height 22)**

&#x20; **N=  10000  query=last    linear=   244.238 us  BST=     0.742 us  (tree height 30)**

&#x20; **N=  10000  query=absent  linear=   155.673 us  BST=     0.953 us  (tree height 30)**

&#x20; **N= 100000  query=last    linear=  2096.544 us  BST=     0.555 us  (tree height 40)**

&#x20; **N= 100000  query=absent  linear=  1656.020 us  BST=     0.577 us  (tree height 40)**



**Linear scan grows with N; BST lookup grows with log N ΓÇö the same**

**win binary search gave you on Floor 1, but now the structure STAYS**

**searchable as you insert and remove, with no re-sort step.**

**One catch: this tree was built from SHUFFLED data. Insert the**

**monsters already sorted and the BST degenerates into a stick**

**(height \~N), and lookup drops right back to linear ΓÇö the problem**

**the next floor's self-balancing tree exists to solve.**



**If the entries were already preordered before being added it would have the shape of a long strand of each child going to the right of teh parent rather than a pyramid of branches. This makes the height as big as the amount of entries included and subsequently not have any of the benefits of a BST for recall because no values were eliminated as you search.** 



6\. One-paragraph reflection. You have now built five containers on pointers — Chain, Stack, Queue, Tree, and BST. This is the first one that is fast because of its shape. What did the ordering rule buy you that the general Tree couldn’t, and what did it cost you (think about remove)? And: the destructor you read on Floor 8, you wrote this week. Did it feel different to write than to read?



**The biggest difference in how a general tree and a BST are navigated is tied to their sorting restrictions. The general tree can have multiple child nodes that don't necessarily have a value sorting requirements. This makes it good for creating and visualizing relationships between data, but less effective at quickly navigating to a particular point of data. The BST shines in this regard because its limit to children means starting from a root can only have you travel at most one of two directions which is determined by the sorting involved in the construction of the tree. This allows us to safely cut away potential paths that were not taken to reduce the total amount of steps in searching for something. The relationships now are less than and greater than, but you lose the ability to make more ambiguous relationships between the nodes. The destructor we wrote for this week was a little bit different than what we had viewed last week because we designate two specific left and right nodes as children nodes instead of a general children nodes bag. Both want to have the children destroyed first so it can preserve their connection until the root is destroyed. This week we constructed it so all the left most nodes would be destroyed first, then the right nodes, then finally the root node. I don't think the order should matter to much as long as it is consistent: I feel like recursing on all the right nodes and then left nodes would accomplish the same goal as long as the root node is left last.** 



