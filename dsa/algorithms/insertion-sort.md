# Insertion sort

![Sorted sections are bordered](insertionsort.gif)

Sorted sections are bordered

- Time complexity : $O(n^2)$
- Stable
- Adaptive

```python
def insertionSort(arr):
    
    n = len(arr)
    
    for i in range(n-1):
        j = i+1
        
        while j >0:
            if arr[j] < arr[j-1]:
                arr[j],arr[j-1] = arr[j-1],arr[j]
                j -= 1
                
            else:
                break
```

- *with double for loops*
    
    ```python
    def insertionSort(arr):
        
        n = len(arr)
        
        for i in range(n-1):
            for j in range(i+1,0,-1):
                if arr[j] < arr[j-1]:
                    arr[j],arr[j-1] = arr[j-1],arr[j]
                    
                    
                else:
                    break
    ```