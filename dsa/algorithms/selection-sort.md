# Selection sort

→ Find smallest → Swap with index at start of search

![selectionsort.gif](selectionsort.gif)

![Untitled](Untitled%2054.png)

- Time complexity : $O(n^2)$
- Unstable
    
    ![Untitled](Untitled%2055.png)
    

![Untitled](Untitled%2056.png)

```python
def selectionSort(arr):
    n = len(arr)
    
    for i in range(n):
        minIndex = i
        
        for j in range(i+1,n):
            if arr[j]<arr[minIndex]:
                minIndex = j
                
        if i != minIndex:
            arr[i],arr[minIndex] = arr[minIndex],arr[i]
```