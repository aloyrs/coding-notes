# External Sorting

External sorting is a class of sorting algorithms that can handle massive amounts of data

# When?

Required when the data being sorted do not fit into the main memory of a computing device (usually RAM)

Eg. only 2GB RAM but 8GB file

# General Idea

1. Break the file into blocks
2. Sort the blocks 
3. Merge the sorted blocks

# Example : **External Merge Sort Algorithm**

1. First, divide the file into runs such that the size of a run is small enough to fit into the main memory.
2. Next, sort each run in main memory using the standard merge sort sorting algorithm.
3. Finally, merge the resulting runs into successively bigger runs until the file is sorted.