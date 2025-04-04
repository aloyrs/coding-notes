# Merge sort

![Continuously divide array by half until left with individual items](mergesort.gif)

Continuously divide array by half until left with individual items

- Time complexity : $O(nlogn)$
- Space complexity : $O(n)$
- A Divide & Conquer algorithm
- Recursive
- Stable

```python
def merge(left, right):
    leftPtr = 0
    rightPtr = 0

    newArr = []

    while leftPtr < len(left) and rightPtr < len(right):
        if left[leftPtr] < right[rightPtr]:
            newArr.append(left[leftPtr])
            leftPtr += 1
        else:
            newArr.append(right[rightPtr])
            rightPtr += 1

    while leftPtr < len(left):
        newArr.append(left[leftPtr])
        leftPtr += 1

    while rightPtr < len(right):
        newArr.append(right[rightPtr])
        rightPtr += 1

    return newArr

def mergeSort(arr):
    # base case
    if len(arr) == 1:
        return arr

    mid = len(arr) // 2
    left = mergeSort(arr[:mid])
    right = mergeSort(arr[mid:])

    merged = merge(left, right)

    return merged

arr = [7, 4, 6, 3, 5, 2, 8]

mergeSort(arr)

print(arr)
```