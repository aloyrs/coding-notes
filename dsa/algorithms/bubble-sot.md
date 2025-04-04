# Bubble sort

![bubblesort.gif](bubblesort.gif)

- Why is it called bubble sort?
    
    larger elements "bubble" up to the top/end of the list
    

[Bubble sort in 2 minutes](https://www.youtube.com/watch?v=xli_FI7CuzA)

![Green line seperates the ‘unsorted | sorted’ sections (unsorted left , sorted right)
1. ‘12’ is largest and bubbled to end 
2. ‘8’ is largest in the unsorted section w/o ‘12’
3. ‘7’ is largest in the unsorted section [w](http://w.io)/o ‘12’ & ‘8’
](Untitled%2053.png)

Green line seperates the ‘unsorted | sorted’ sections (unsorted left , sorted right)
1. ‘12’ is largest and bubbled to end 
2. ‘8’ is largest in the unsorted section w/o ‘12’
3. ‘7’ is largest in the unsorted section [w](http://w.io)/o ‘12’ & ‘8’

- Compare consecutive indices
- Swap the index if larger one is on the left
- Largest index will bubble all the way right to the last index with each iteration
- Sorted section will form at end of array

- Time complexity : $O(n^2)$
- Stable sorting algorithm