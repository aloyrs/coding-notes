# Kadane’s Algorithm

# >>> Maximum Contiguous Sub-Array Sum <<<

---

![Untitled](Untitled%2038.png)

Time complexity - O(n)

- Add num of current iteration to currSum
- If currSum < 0 , then should not be added to next number → cos it will only decrease the currSum
- currSum should be set to 0

![Untitled](Untitled%2039.png)