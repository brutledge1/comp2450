1. A transcript of the demo above, pasted from your terminal.

> search Goblin
Goblin   HP 8   ATK 2   weakness: fire
> search Iron key
 Iron key (wt 0.1, val 0)
> inventory
   1.  Rusty sword       (wt 4.0, val 5)
   2.  Healing potion    (wt 0.5, val 12)
   3.  Iron key          (wt 0.1, val 0)
   4.  Loaf of bread     (wt 0.1, val 1)
   5.  Cloak of shadows  (wt 1.5, val 80)
> inspect 3
  Iron key  (wt 0.1, val 0)
> inspect 99
No such item. (index 98 out of bounds for size 5)
> sort inventory by weight
   1.  Iron key          (wt 0.1, val 0)
   2.  Loaf of bread     (wt 0.1, val 1)
   3.  Healing potion    (wt 0.5, val 12)
   4.  Cloak of shadows  (wt 1.5, val 80)
   5.  Rusty sword       (wt 4.0, val 5)
> benchmark sort 10000
  N=  10000  mergeSort= 108.398 ms  quicksort=   71.762 ms  std::sort=  49.295 ms

2. Instantiate Bag<int> in a throwaway test and call findByName on it. Paste the full compiler error. Circle (or describe) the one line that actually tells you what's wrong. Why is this harder to read than a normal type error, and what does that tell you about templates?

Output:
  FAILED: [code=2] CMakeFiles/the_descent.dir/main.cpp.obj 
  C:\PROGRA~1\MICROS~4\18\COMMUN~1\VC\Tools\MSVC\1451~1.362\bin\Hostx64\x64\cl.exe  /nologo /TP   /DWIN32 /D_WINDOWS /GR /EHsc /Zi /Ob0 /Od /RTC1 -std:c++17 -MDd /W4 /showIncludes /FoCMakeFiles\the_descent.dir\main.cpp.obj /FdCMakeFiles\the_descent.dir\ /FS -c C:\Users\benja\OneDrive\Documents\GitHub\comp2450\project\floor-03-starter\main.cpp
C:\Users\benja\OneDrive\Documents\GitHub\comp2450\project\floor-03-starter\bestiary\Search.h(74): error C2228: left of '.name' must have class/struct/union
  C:\Users\benja\OneDrive\Documents\GitHub\comp2450\project\floor-03-starter\bestiary/Search.h(74): note: type is 'const int'
  C:\Users\benja\OneDrive\Documents\GitHub\comp2450\project\floor-03-starter\bestiary/Search.h(74): note: the template instantiation context (the oldest one first) is
  C:\Users\benja\OneDrive\Documents\GitHub\comp2450\project\floor-03-starter\main.cpp(90): note: see reference to function template instantiation 'const T *dungeon::findByName<int>(const dungeon::Bag<T> &,const std::string &)' being compiled
          with
          [
              T=int
          ]
  ninja: build stopped: subcommand failed.

Actual Error:
	left of '.name' must have class/struct/union
	The code we implemented was:
	Bag<int> numbers;
   	findByName(numbers, "seven");
	
	The T we called did not have a member called name to be called on so it could be evaluated. This was harder to read than other errors and goes to show that while templates are a powerful tool it is important that they have contingency built in when fed the wrong format of information.
	

3. Swap .at() for [] in the inspect command. Pass a bad index. Describe what the program does now — does it crash? Print garbage? Silently return? Restore .at() when done. One sentence: when would you ever want operator[] over .at() in production?

The program crashes; If there is no way to go out of bounds you might want to use [] over .at(), but it seems to be a safer practice to use the .at() method. 

4. Remove the try/catch around the main loop. Trigger a bad inspect. Describe exactly what you see on stderr — the unhandled-exception message the runtime prints before std::terminate. Put the catch back. Then try the anti-pattern catch (...) { } (empty body) and describe what is now worse than having no catch at all.

Error Message: Unhandled exception at 0x00007FFA7D5441CA in the_descent.exe: Microsoft C++ exception: dungeon::BagException at memory location 0x000000795F4FF550.

I tried to implement the anti-pattern catch and it allowed me to continue using the program without kicking me out despite not giving any feedback. I suppose not being forced out does give the impression that nothing went wrong despite trying to access an invalid field. 

5. Change BagException so it does NOT inherit from std::exception. What still compiles? What behavior (if any) do you lose? One sentence on why inheriting from std::exception is the right default.

The search, list, inventory, inspect (if in range), and the sort inventory functions still worked. It lost the ability to inspect outside of range without crashing. Having exception by default allows the program to change how it handles errors.

