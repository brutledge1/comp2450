1\. A transcript of the demo above (your own hero name). Include lookup of three creatures, one of them not in the bestiary (lookup Drake works), and at least one strike. (Your benchmark names microseconds will not match the page; that’s fine.)



> selftest registry

&#x20; index: size==5, distinct weaknesses==3, count\[holy]==3: OK

&#x20; knows: Lich present, Drake absent: OK

&#x20; recall: Wraith->hp==14, Drake==nullptr: OK

&#x20; hasWeakness: holy present, water absent: OK

&#x20; countWeakness: holy==3, water==0: OK

&#x20; forget: drop a shared weakness (count--), drop a last weakness (erased), absent==false: OK

&#x20; all phases OK

> knows Lich

&#x20; McCown knows 'Lich'.

> knowss Drake

McCown does not recognize 'knowss'. Try `help`.

> weaknesses

&#x20; blunt  (2 monsters)

&#x20; fire  (6 monsters)

&#x20; holy  (3 monsters)

&#x20; light  (2 monsters)

&#x20; slashing  (1 monsters)

&#x20; water  (1 monsters)

&#x20; (6 distinct weaknesses)

> lookup Goblin

Goblin   HP 8   ATK 2   weakness: fire

&#x20; (looked up in the Registry)

> lookup Stone Sentinel

Stone Sentinel   HP 30   ATK 5   weakness: blunt

&#x20; (looked up in the Registry)

> lookup Lost One

&#x20; 'Lost One' is not in the Hall of Names.

> weakness fire

&#x20; 6 monsters fear fire.

> names

Bone Spider   HP 6   ATK 2   weakness: fire

Cave Troll   HP 28   ATK 7   weakness: fire

Cinder Bat   HP 4   ATK 1   weakness: water

Frostmaw   HP 22   ATK 6   weakness: fire

Goblin   HP 8   ATK 2   weakness: fire

Ironclaw Bear   HP 24   ATK 5   weakness: slashing

Lich   HP 35   ATK 6   weakness: holy

Marsh Lurker   HP 18   ATK 3   weakness: fire

Necrothrall   HP 16   ATK 4   weakness: light

Ratking   HP 9   ATK 2   weakness: fire

Shadow Hound   HP 12   ATK 4   weakness: light

Skeleton   HP 10   ATK 3   weakness: blunt

Stone Sentinel   HP 30   ATK 5   weakness: blunt

Wisp   HP 3   ATK 1   weakness: holy

Wraith   HP 14   ATK 4   weakness: holy

&#x20; (15 names, alphabetical ΓÇö std::map keeps them ordered)

> strike Goblin

&#x20; Struck 'Goblin' from the Hall of Names. (14 remain.)

> weakness fire

&#x20; 5 monsters fear fire.

> recall Goblin

Goblin   HP 8   ATK 2   weakness: fire

&#x20; (recalled from the tree)

> benchmark names



\-- The Hall of Names: linear scan vs BST vs std::map (1000 iterations per cell) --

&#x20; N=    100  query=last    linear=     3.290 us  BST=   0.379 us  std::map=   1.312 us  (tree height 13)

&#x20; N=    100  query=absent  linear=     1.223 us  BST=   0.226 us  std::map=   0.776 us  (tree height 13)

&#x20; N=   1000  query=last    linear=    19.624 us  BST=   0.599 us  std::map=   1.630 us  (tree height 22)

&#x20; N=   1000  query=absent  linear=    14.898 us  BST=   0.611 us  std::map=   1.172 us  (tree height 22)

&#x20; N=  10000  query=last    linear=   235.893 us  BST=   0.720 us  std::map=   1.414 us  (tree height 30)

&#x20; N=  10000  query=absent  linear=   168.194 us  BST=   0.679 us  std::map=   1.290 us  (tree height 30)

&#x20; N= 100000  query=last    linear=  2074.898 us  BST=   0.561 us  std::map=   1.723 us  (tree height 40)

&#x20; N= 100000  query=absent  linear=  1634.537 us  BST=   0.734 us  std::map=   2.319 us  (tree height 40)



std::map::find tracks the BST ΓÇö both grow with log N, both crush

the linear scan. The difference is the code: the BST was a class you

wrote across a whole floor; std::map was one declaration. And unlike

your plain BST, std::map is balanced (a red-black tree), so it NEVER

degenerates into a stick ΓÇö the library gives you the balanced tree of

Floor 9┬╜ and a key->value index on top of it, for free.



> quit

McCown notes your departure. "You leave in order."



2\. Set or map? Each question below is one line of code against one of the Registry’s three containers (byName\_, weaknesses\_, weaknessCounts\_). For each, write that line — the way it would appear inside a Registry method — for example weaknesses\_.count("fire") > 0. (a) Does McCown know a monster named Wisp? (b) What is Wisp’s attack? (c) Does anything fear light? (d) How many monsters fear holy? Then one sentence: when do you want a std::set instead of a std::map?



A) byName\_.count("Wisp")

B) byName\_.find("Wisp")
C) weaknesses\_.count("light")

D) weaknessCounts\_.find("holy")

You would use a std::set when you only care about the value stored and not related properties. Maps have keys that point to additional values while the sets values are just the keys.



3\. Sorted for free, and the const key. Run names. The monsters went in in file order (Goblin, Wraith, Skeleton, …). In one or two sentences: why do they come out alphabetical with no sort in your code, and which earlier floor had you build that same kind of structure by hand? Then: each element of the map is a std::pair<const std::string, Monster>, and the name is const. Suppose you could rename the "Bone Spider" key to "Zombie" without moving it. Where in the map would "Zombie" be sitting, and why would find("Zombie") then miss it?



The std::set has the values sorted by default when they are added and this structure is similar to what was built on floor 9 with the binary search trees. Zombie would be found near the beginning of the map and would be missed when searched for because the find function would normally safely assume that anything near the beginning of the list should be come alphabetically before the values in the middle and after of the map.



4\. recall, then and now. Open hero/BST.h and find findFrom: that recursive descent was Floor 9’s recall. This week recall is one map::find. Name one thing you gained by switching and one thing you gave up.



The map::find function is more concise to write than the full function of findFrom and if I remember correctly also tended to run quicker. One downside might be that the function we wrote used an auto template type value for the parameter while map::find is tied to the type of key the map depends on. The self made function could work with either numerical or alphabetical sorting depending on the values of the tree, but you need to be more conscious that what you are passing to the standard function matches the values of the map.



5\. The Phantom Key — try it. In countWeakness, temporarily replace the two-line body with return weaknessCounts\_\[w]; and build. Paste the first error line. Then put the find version back and rebuild. In your own words: (a) what does \[] do when the key isn’t in the map, and (b) why won’t the compiler let you use it here?



First error message was: no operator "\[]" matches these operands. Wasn't sure if that was the intended message so second error is:

&#x20;

binary '\[': no operator found which takes a left-hand operand of type 'const std::map<std::string,int,std::less<std::string>,std::allocator<std::pair<const std::string,int>>>' (or there is no acceptable conversion)



A) If the key isn't in the map it wants to add that as an entry to the map. 

B) The const keyword at the end of int countWeakness(const std::string\& w) const makes the function read only. 



6\. Three views, one source. After strike Goblin, names no longer lists Goblin, but recall Goblin (the Floor 9 tree command) still finds it. In one or two sentences: why is that correct, not a bug?



The Goblin is removed from the map byName but it doesn't remove it from the BST where it was included in floor 9. 



7\. One-paragraph reflection. The Registry keeps every name in alphabetical order whether you need it or not. Name one command from this week that used that order and one that didn’t need it at all. If all you ever asked was “is this name here?”, would keeping the order be worth paying for? (Floor 11 is about giving it up.)



The forget command removes an entry but then keeps the same ordering as it had before. Something like the knows command only looks to see if the entry exists. In a set/map each entry is unique so it only has to see if it pops up once. Being in order doesn't necessarily save time because we designed the know as a descent where we would start from one end and travel linearly to the other. Regardless it only needs to know it exists once and it could take up to as long as the last entry in this scenario. Just asking if something exists doesn't necessarily require for the it to be ordered in a particular manner. 

