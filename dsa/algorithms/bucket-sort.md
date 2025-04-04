# Bucket sort

# When ?

Useful when input is uniformly distributed over a range

![Untitled](Untitled%2059.png)

```python
bucketSort()

  create N buckets each of which can hold a range of values
  for all the buckets
    initialize each bucket with 0 values
  for all the buckets
    put elements into buckets matching the range
  for all the buckets 
    sort elements in each bucket
  gather elements from each bucket
end bucketSort
```

- ChatGPT Explanation
    
    Bucket Sort: This algorithm works by dividing the range of input values into a set of buckets, then distributing the elements into the buckets based on their value. After that, it sorts the elements in each bucket separately using any sorting algorithm and then concatenates the sorted buckets to obtain the final sorted array. It has a linear time complexity of O(n + k), where k is the number of buckets.