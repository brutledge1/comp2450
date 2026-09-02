Lab
1. The full `benchmark` output (paste from your terminal).

-- Race the Bestiary (1000 iterations per cell) --
  N=     10  query=last    linear=     0.591 us  binary=   0.342 us  recursive=   0.331 us
  N=     10  query=absent  linear=     0.256 us  binary=   0.185 us  recursive=   0.193 us
  N=    100  query=last    linear=     2.464 us  binary=   0.263 us  recursive=   0.270 us
  N=    100  query=absent  linear=     1.846 us  binary=   0.210 us  recursive=   0.220 us
  N=   1000  query=last    linear=    21.088 us  binary=   0.407 us  recursive=   0.414 us
  N=   1000  query=absent  linear=    13.887 us  binary=   0.321 us  recursive=   0.321 us
  N=  10000  query=last    linear=   206.215 us  binary=   0.612 us  recursive=   0.646 us
  N=  10000  query=absent  linear=   141.281 us  binary=   0.640 us  recursive=   0.701 us
  N= 100000  query=last    linear=  2254.648 us  binary=   0.725 us  recursive=   0.785 us
  N= 100000  query=absent  linear=  1610.557 us  binary=   1.268 us  recursive=   1.342 us

2. **At what bestiary size does binary search start to clearly beat linear?** Read your table; pick a row.

Clearest at N = 100. Actually faster at N = 10.

3. **For N=10, which is faster, and why might that surprise a beginner?** (Hint: count what each algorithm actually does at small N.)

The Binary is faster than Linear. I think beginners might assume smaller numbers would see linear checking first, but in the worst case Linear would have to do 10 checks while binary would have to do 3 to 4. Linear:(1,2,3,4,5,6,7,8,9,10) Binary:(5,7,9,10)

4. **What happens when you call `binarySearch` on the *unsorted* bestiary?** Try it: comment out the `sortBestiary(bestiary);` call in `main.cpp`, rebuild, run `search Goblin` and `search Wraith`. Restore `sortBestiary` when done.

Unable to find the searched items because it narrows down the list with a comparison of higher and lower values. 

5. **Iterative vs. recursive binary search** — do their per-call times differ in your benchmark? By how much? Why might that be? (Think about what extra work happens when you call a function.)

The times vary slightly. It oddly looks like recursive takes slightly longer (anywhere from 0.01 - 0.1 us), which may be because of the base case being tested. I assume it would be quicker if it wasn't checking up to the last entry or not finding it at all.

Commit `lab-notes.md` along with your code. Your commit history should show at least three commits this week — Mon (linear), Wed (iterative binary), Fri (recursive + lab).
