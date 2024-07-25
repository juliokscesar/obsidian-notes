# Definitions
## Algorithm
Informally, an algorithm is a well-defined computational procedure that takes some value, or set of values, as ***input*** and produces some value, or set of values, as ***output***. It is a tool for solving a well-specified computational problem.

## Data structures
A data structure is a way to store and organize data in order to facilitate access and modifications.

## NP-Complete problems
Hard problems that have no efficient algorithm known. 

## Parallelism
Working with several processing cores all at once - "multithreaded" algorithms.

# Insertion Sort
An efficient algorithm for sorting a *small* number of elements. It works like the way people sorte a hand of playing cards: we start with an empty left hand and then remove one card at a time from the table and insert it into the correct position in the left hand. To find the correct position, we compare it with each of the cards already in the hand.
Given an input array *A*, the algorithm sorts the input numbers *in place*: it rearranges the numbers within the array *A*. For example, given an array `A = {5, 2, 4, 6, 1, 3}`:
![[Pasted image 20240723103907.png]]
In each iteration, the black rectangle holds the key taken from `A[j]`, which is compared with the values in shaded rectangles to its left in the test. Shaded arrows show array values moved on position to the right. And black arrows indicate where the key moves to.
The pseudo-code for *Insertion-sort* in a given array `A[1..A.length]` is:
```
// Insertion-Sort(A)
for j=2 to A.length:
	key = A[j]
	i = j-1 // Start checking from the element on the left of the key
	while i > 0 and A[i] > key: // go through every element on the left if its bigger then the key
		A[i + 1] = A[i] // move one to the right
		i = i - 1 // then check for the next-left

	A[i + 1] = key // A[i] is the element less than the key. 

```



# Binary Search
Binary search is an algorithm to solve *search problems*. Its input is a *sorted* list of elements, and if the element you're looking for is in that list, binary search returns the position where it's located. Otherwise, it returns null (or like -1).

Binary search works by taking the list and checking first for the middle element. If its less than the desired element you're looking first, it cuts the first half of the list and then looks for the middle element of the remaining half. If that new middle element is, say, higher than the desired element, then it cuts the second half and looks for the middle element of remaining half.
In summary, it keeps cutting the (sorted) list in half until it finds the desired element.



# Linear search (or Sequential search)
The name explains a lot. Instead of, like the binary search, starting from the middle and keep cutting the list, Linear search will start from the first element and then keep advancing one step at a time until it finds the desired element.

This is the simplest search algorithm. The best advantage is that it doesn't require the input list to be sorted, but it can be slow.