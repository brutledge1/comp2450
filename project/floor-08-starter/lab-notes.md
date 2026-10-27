1\. A transcript of the demo above (with your own hero name; run lineage on at least three different creatures, one of them a category like Beasts).



**> selftest tree**

&#x20; **empty Tree<int>: empty() \&\& size==0 \&\& height==0: OK**

&#x20; **addChild: root==1 with 3 children: OK**

&#x20; **size()==7 over the sample tree: OK**

&#x20; **height()==2 (longest path 1->2->5): OK**

&#x20; **preOrder == {1,2,5,6,3,4,7} (depth-first): OK**

&#x20; **levelOrder == {1,2,3,4,5,6,7} (breadth-first): OK**

&#x20; **lineage(6)=={1,2,6} and lineage(404) empty: OK**

&#x20; **all phases OK**

**> taxonomy**

**Creatures of the Hold**

&#x20;   **- Undead**

&#x20;       **- Corporeal**

&#x20;           **- Skeleton**

&#x20;           **- Necrothrall**

&#x20;           **- Lich**

&#x20;       **- Incorporeal**

&#x20;           **- Wraith**

&#x20;           **- Wisp**

&#x20;   **- Beasts**

&#x20;       **- Mammals**

&#x20;           **- Shadow Hound**

&#x20;           **- Ironclaw Bear**

&#x20;           **- Cinder Bat**

&#x20;       **- Giants**

&#x20;           **- Cave Troll**

&#x20;           **- Frostmaw**

&#x20;   **- Vermin**

&#x20;       **- Bone Spider**

&#x20;       **- Ratking**

&#x20;       **- Marsh Lurker**

&#x20;   **- Constructs**

&#x20;       **- Stone Sentinel**

&#x20; **(23 creatures and categories; height 3)**

**> taxonomy --bfs**

&#x20; **breadth-first (level-order):**

&#x20;   **Creatures of the Hold**

&#x20;   **Undead**

&#x20;   **Beasts**

&#x20;   **Vermin**

&#x20;   **Constructs**

&#x20;   **Corporeal**

&#x20;   **Incorporeal**

&#x20;   **Mammals**

&#x20;   **Giants**

&#x20;   **Bone Spider**

&#x20;   **Ratking**

&#x20;   **Marsh Lurker**

&#x20;   **Stone Sentinel**

&#x20;   **Skeleton**

&#x20;   **Necrothrall**

&#x20;   **Lich**

&#x20;   **Wraith**

&#x20;   **Wisp**

&#x20;   **Shadow Hound**

&#x20;   **Ironclaw Bear**

&#x20;   **Cinder Bat**

&#x20;   **Cave Troll**

&#x20;   **Frostmaw**

**> lineage Lich**

&#x20; **Creatures of the Hold > Undead > Corporeal > Lich**

**> lineage Goblin**

&#x20; **'Goblin' is not in McCown's catalogue.**

**> quit**

**McCown notes your departure on the chart. "You leave classified."**



2\. The recursion skeleton, in your words. Write countFrom, heightFrom, and preOrderInto out and circle the three parts they share: the nullptr base case, the act-on-this-node line, the recurse-into-children loop. In two sentences: what is the one thing that differs between counting, measuring height, and listing pre-order?



**The recursion skeleton consists of a base case, what to do if the base case is false, and a way of looping back into the same function by calling itself as long as a condition holds true. For the recursion functions we built the main thing that separates them is the ways they modify what to return. All three have a base case with the node being nullptr (except height also considers the children.size()), and each one recurses by setting up a for loop that continues until there are no children nodes left. The countFrom function assumes if there n == nullptr the total is at least 1, and this total is incremented inside the recursive statement for each children included (Effectively counts all nodes in the subtree specified). The heightFrom function takes the max height with a base case of 0, and each time it loops through the children it increments the height by 1 in the return case. That means the heightFrom can return a case of 0 if it has no children, but the countFrom will always have a value of at least one. The last function preOrderInto has a pass by reference vector to keep track of the order of children it reads. It does this by pushing the data of the node into the out vector then looping for each child. This modification happens before the recursive loop is called.**



3\. DFS vs BFS by hand. On paper, take the sample tree from selftest tree and write out both the pre-order and the level-order sequences before you run them. Then run taxonomy --dfs and --bfs on the real taxonomy and confirm your hand-trace logic. One sentence: which node moved the most positions between the two orders, and why?



**The Constructs node moved the most between the two orders. In the depth first it was found in the next to last position because it was the right most child (last) of Creatures of the Hold so it had to wait until all the previous children on the same level and all of their children were accounted for first. In the breadth classification you would you continue to the next level after all of the previous children of the same level were accounted for. This meant that being on the second level it only had to wait for the other nodes of the same level: undead, beast, and vermin.**



4\. The missing Goblin. lineage Goblin reports “not classified” — McCown never finished filing Grix’s kin. Add the Goblin to data/taxonomy.txt under a sensible branch (your call — argue for it in one sentence). Rebuild, run lineage Goblin, paste the result. Did you have to recompile any .cpp, or just edit the data? Why does that distinction matter?



**I included Goblin under the Vermin branch because it was living unlike the Undead and Constructs Branch, and didn't share enough of the same qualities as the Beast branches. It wouldn't initially work because I didn't rebuild the project but after doing so I received this result. This signifies that once a tree is built it can't have its contents changed until it is rebuilt.**



**> lineage Goblin**

&#x20; **Creatures of the Hold > Vermin > Goblin**





5\. Post-order, then put it back. Change preOrderInto to push the node after the loop instead of before. Run taxonomy --dfs, paste the new order, and explain in one sentence what changed and why this is now called post-order. Restore pre-order.



**> taxonomy --dfs**

&#x20; **depth-first (pre-order):**

&#x20;   **Skeleton**

&#x20;   **Necrothrall**

&#x20;   **Lich**

&#x20;   **Corporeal**

&#x20;   **Wraith**

&#x20;   **Wisp**

&#x20;   **Incorporeal**

&#x20;   **Undead**

&#x20;   **Shadow Hound**

&#x20;   **Ironclaw Bear**

&#x20;   **Cinder Bat**

&#x20;   **Mammals**

&#x20;   **Cave Troll**

&#x20;   **Frostmaw**

&#x20;   **Giants**

&#x20;   **Beasts**

&#x20;   **Bone Spider**

&#x20;   **Ratking**

&#x20;   **Marsh Lurker**

&#x20;   **Goblin**

&#x20;   **Vermin**

&#x20;   **Stone Sentinel**

&#x20;   **Constructs**

&#x20;   **Creatures of the Hold**



**It posted it in a weird reverse order. Now the root node which is usually first was returned last. This pattern holds true where the children are given before the parent nodes.**



6\. Why this tree is slow to search. Add a temporary counter to findFrom that counts how many nodes it visits, and call lineage on the last leaf in the file. How many nodes did it check? In two sentences: why does a general tree give you no search speedup over McCown’s old flat list — and what single rule would the structure need before search could skip whole branches? (You are describing a BST. That’s next floor.)



**> lineage Stone Sentinel**

**Visited 24 nodes.**



**Because it is doesn't have a way of comparing which node to descend on, it will check all of the children nodes before sweeping to the next node. If there was a way of checking the alphabetical values of the node we are searching for then it would be able to discern whether to visit that node and subsequently its children (given the nodes follow a value order).**



7\. One-paragraph reflection. You have now built four containers on top of pointers — Chain, Stack, Queue, and Tree. The first three were lines; this one branches. What felt genuinely new about the tree, and what felt like the same lesson as before? (Heads up: the destructor you read this week, you will write next week, because a BST owns its nodes the same way.)



**The usage of nodes is still very prevalent in the Tree as it was with the Chain, Stack, and Queue. They are all still concerned with return information in a certain format, but how they do so differs. Chain felt like it moved in one direction, the Stack made use of last in first out like how you would grabbing a plate from the top, and Queue used first in first out like you would expect from standing in a line to have your order taken. The Tree was interesting because it had several different ways of returning information as well as the implementation of multiple potential children node instead of a one to one. This structure introduced the breadth first and depth first searches where it prioritized either sweeping each level before moving to the next or ensuring all children nodes were accounted for before jumping back to a "sibling node" (a node found on the same level).** 

