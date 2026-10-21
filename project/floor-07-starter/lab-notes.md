1. A transcript of the demo above (with your own hero name and your own choice of provoked enemies).



**> selftest queue**

&#x20; **empty Queue<int>: size==0 \&\& empty(): OK**

&#x20; **enqueue(7): size==1 \&\& front()==7: OK**

&#x20; **enqueue 1,2,3: size==3 \&\& front()==1 (FIFO): OK**

&#x20; **after dequeue(): size==2 \&\& front()==2: OK**

&#x20; **drain to empty: size==0 \&\& empty(): OK**

&#x20; **all phases OK**

**>**

**> potato A B C D E 3**

&#x20; **Survivor: D**

**> potato Grix Skrit Quill Vael Resh 2**

&#x20; **Survivor: Quill**

**> potato OnlyOne 7**

&#x20; **Survivor: OnlyOne**

**>**

**> provoke Fellow1**

&#x20; **Fellow1 takes a number and joins the line.**

**> provoke Fiend2**

&#x20; **Fiend2 takes a number and joins the line.**

**> provoke Friendly3**

&#x20; **Friendly3 takes a number and joins the line.**

**> simulate**

**Turn 1: Fellow1 stirs in the dark.**

**Turn 2: Fiend2 stirs in the dark.**

**Turn 3: Friendly3 stirs in the dark.**

**All enemeis have acted. The line is empty.**

**> simulate**

**No enemies in the line. Use provoke <name> first.**

**> quit**

**Quill stamps your ticket. The line shuffles forward by one.**



2\. Same chain, different ends. Open your Floor 6 hero/Stack.h and your Floor 7 hero/Queue.h side by side and fill in this table with the Chain<T> method each one calls:





|**Job**|**Stack<T> calls…**|**Queue<T> calls…**|
|-|-|-|
|**add an item (push / enqueue)**|**chain\_.push\_front(value);**|**chain\_.push\_back(value);**|
|**remove an item (pop / dequeue)**|**chain\_.pop\_front();**|**chain\_.pop\_front();**|
|**read the next item out (top / front)**|**return chain\_.head()->data;**|**return chain\_.head()->data;**|



&#x09; 	 

Then finish two sentences: “A stack and a queue are different because…” and “Queue uses a Chain<T> instead of a Bag<T> because…” (the comment at the top of Queue.h answers the second one).



**A stack and a queue are different because a stack follows the convention of last in - first out while a queue uses first in - first out.** 



**Queue uses a Chain<T> instead of a Bag<T> because the convention of adding to one end and removing have differing Big O Notations. A Bag<T> is just a wrapper for a vector so when we call a pop\_front function it would have to shift each individual element by one making it O(n) while the Chain<T> has O(1).** 



3\. Grix’s shortcut. Grix says to skip the line and enqueue at the front. Try it: in hero/Queue.h, change the one word in enqueue from chain\_.push\_back(value); to chain\_.push\_front(value);. Build, then run selftest queue and potato A B C D E 3. Paste both outputs. In one sentence: what did you actually build? Change the word back, rebuild, and run selftest queue once more to confirm all phases are OK again.



**> selftest queue**

&#x20; **empty Queue<int>: size==0 \&\& empty(): OK**

&#x20; **enqueue(7): size==1 \&\& front()==7: OK**

&#x20; **enqueue 1,2,3: size==3 \&\& front()==1 (FIFO): FAIL ΓÇö front() did not return the FIRST enqueued value ΓÇö enqueue/front are on the same end (that's a stack, not a queue)**

&#x20; **after dequeue(): size==2 \&\& front()==2: OK**

&#x20; **drain to empty: size==0 \&\& empty(): OK**

&#x20; **(see FAILs above)**

**> potato A B C D E 3**

&#x20; **Survivor: A**



**Making this adjustment changed the Queue<T> into a Stack<T> by utilizing LIFO.**



Optional bonus: Phase 4 still says OK even with Grix’s version. Why did it pass by luck?



**Because there were only 3 elements and the middle element's value was the same in both scenarios removing the first element should always return OK. Ex.**

**3, 2, 1 -> 2, 1 (Size of 2; the front is 2)**

**1, 2, 3 -> 2, 3 (Size of 2; the front is 2)**



4\. Pass the potato by hand. Before you run it, predict the survivor of potato A B C D 2 on paper. Write the queue after each step (front on the left). The first two rows are done for you:



**Prediction: A should remain**



start:               A B C D

rotate (A to back):  B C D A

**eliminate B:         C D A**

**rotate (C to back):  D A C**

**eliminate D: 	     A C**

**rotate (A to back):  C A**

**eliminate C:         A**



Keep going until one name is left. Then run potato A B C D 2 and paste the output. Did your trace match?



**> potato A B C D 2**

&#x20; **Survivor: A**



**The trace appeared to match.**



5\. Short reflection (two or three sentences). You wrote the same kind of thing two weeks in a row: a small adapter that puts a contract on top of a Chain<T>. What felt easier the second time?



**In the previous week in which we established the Chain<T> to use for our Stack<T>, I had trouble making the difference between the two. This time around when we used the same Chain<T> for our Queue<T> I was more easily able to observe that it is more so about the rules and constraints we apply to these structures that give them significance. By just adjusting where we push our values onto the Chain we can make a structure similar to stacked plates where you take one off the top or a structure like a line in a coffee shop where it is first come first served.** 

