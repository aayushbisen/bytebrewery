---
layout: post
title: Binary Search 👋
date: 2024-01-12 03:00:00 +0900
description: Binary Search Implementation
categories: [Data Structures and Algorithms]
tags: [blog, coding, computer-science , notes, computer, data-structures-and-algorithms-for-coding-interview, data-structures,algorithms, interview, coding-interview, dsalgo, leetcode, gfg, geeksforgeeks, dsa, binary-search]
math: false
mermaid: false
image:
  path: https://github.com/rahulkumarsahu/rahulkumarsahu.github.io/blob/main/assets/binary_search.jpg
  width: 660
  height: 132
  alt: Binary Search
---

# Problem 1: Binary Search Algorithm
<!-- ![udp segment](/assets/binary_search.jpg) -->

## What is Binary Search?

Binary search is an efficient algorithm for finding a target value within a sorted array or list. It works by repeatedly dividing the search space in half. It is a divide-and-conquer algorithm, reducing the problem size in each step.

## Conditions for Binary Search:
* The list must be sorted.
* Access to any element of the data structure takes constant time.

## How Binary Search Works:
Binary search works by repeatedly dividing the search space in half. This ensures that, with each comparison, the search space is reduced by half. As a result, binary search has a time complexity of O(log n), making it more efficient than linear search for large datasets.

## Binary Search Algorithm:
The basic idea of the binary search algorithm can be summarized in the following steps:

* Initialize two pointers, low and high, to the start and end of the sorted array, respectively.
* Calculate the middle index as (low + high) / 2.
* Compare the middle element with the target value.
    * If the middle element is equal to the target, return its index.
    * If the middle element is greater than the target, update the high pointer to mid - 1.
    * If the middle element is less than the target, update the low pointer to mid + 1.
* Repeat steps 2-3 until the target is found or the search space is empty.

## Iterative Binary Search Algorithm:

```java
// O(logN)
public class BinarySearch {

    public static void main(String[] args) {
        int[] sortedArray = new int[]{ 5, 6, 7, 8, 9, 10 };
        int numberToSearch = 8;
        int index = binarySearch(sortedArray, numberToSearch);
        System.out.println(index);
    }

    private static int binarySearch(int[] sortedArray, int target) {
        // array index start from 0 and end index will be one less than length;
        int startIndex = 0;
        int endIndex = sortedArray.length - 1;
        // to find the mid-value
        int midIndex = startIndex + (endIndex - startIndex) / 2;

        // continue till startIndex is <= endIndex
        while (startIndex <= endIndex) {
            //found in a middle element
            if(sortedArray[midIndex] == target) {
                return midIndex;
            } else if (sortedArray[midIndex] < target) {
                // if mid-element is < then increase min because it will be in right side
                startIndex = midIndex + 1;
            } else {
                // if mid-element is > then reduce max because it will be in left side
                endIndex = midIndex - 1;
            }

            midIndex = startIndex + (endIndex - startIndex) / 2;

        }

        return -1;

    }

}
```

## Recursive Binary Search Algorithm:
``` java
public class Application {
    public static int binarySearch(int arr[], int start, int end, int key)
    {
        if (end >= start) {
            int mid = start + (end - start) / 2;

            // If the element is present at the
            // middle itself
            if (arr[mid] == key)
                return mid;

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > key)
                return binarySearch(arr, start, mid - 1, key);

            // Else the element can only be present
            // in right subarray
            return binarySearch(arr, mid + 1, end, key);
        }

        // We reach here when element is not present
        // in array
        return -1;
    }

    public static void main(String args[]) {

        int arr[] = { 2, 3, 4, 10, 40 };
        int length = arr.length;
        int key = 10;
        int result = binarySearch(arr, 0, length - 1, key);
        if (result == -1)
            System.out.println(
                    "Element is not present in array");
        else
            System.out.println(
                    "Element is present at index " + result);
    }
}
```


## Complexity Analysis of Binary Search:

* Time Complexity:
* Best Case: O(1)
* Average Case: O(log N)
* Worst Case: O(log N)
* Auxiliary Space: O(1), If the recursive call stack is considered then the auxiliary space will be O(logN).

## Advantages of Binary Search:

* Efficiency: Binary search is more efficient than linear search, especially for large datasets, due to its logarithmic time complexity.
* Simplicity: The algorithm is relatively simple to implement.
* Memory Efficiency: Binary search typically uses constant space, as it doesn't require additional memory for storing intermediate results.

## Disadvantages of Binary Search:

* Sorted Data Requirement: The data must be sorted for binary search to work. If the data is unsorted, a sorting step is needed before applying binary search.
* Array Requirement: Binary search is best suited for data structures that allow constant-time random access, such as arrays. It may not be as effective for linked lists.

## Applications of Binary Search:

* Searching: The primary application is in searching for a specific element in a sorted array or list.
* Data Retrieval: It can be used in databases to efficiently retrieve data based on sorted keys.
* Range Queries: Binary search is often used in range queries, where you need to find elements within a specific range.
* Spell Checking: In spell-checking algorithms, binary search can be used to quickly identify whether a word is in a dictionary.

# Problems on Binary Search

### Question 1

Problem Statement :- [**First Bad Version**](https://leetcode.com/problems/first-bad-version/description/)

* For this question we have given a number n which denotes how many commits have been made and there is one faulty commit present in between 1 to n commits so we have to find that fault commit and one method isBadVersion() is given which returns whether version is bad version.
* For Solution we have defined our search space 1 to n and applied binary search according to the below code if it is a bad version then we are making **end = mid** why? because that **mid** can be the starting point of a bad version or it is before that so for that reason we are doing this and if it is not a bad version then **start = mid + 1** because if **mid** is not a bad version then there is a possibility after mid only fault commit will be present.

```java
public class Solution extends VersionControl {
    
    public int firstBadVersion(int n) {

        int start = 1;
        int end = n;

        while(start < end) {

            int mid = start + (end - start) / 2;

            if(isBadVersion(mid)) {

                end = mid;

            } else {

                start = mid + 1;

            }
        }

        return start;
    }
}
```

### Question 2
Problem Statement :- [**Search Insert Position**](https://leetcode.com/problems/search-insert-position/description/)

* The problem statement typically involves finding the position at which a target element should be inserted in a sorted array to maintain its sorted order.

* The searchInsert function takes an array nums and a target element target.
* It uses binary search to efficiently find the target element or determine the position at which the target should be inserted.
* The low and high pointers are initially set to the start and end of the array, respectively.
* In each iteration, it calculates the middle index mid and compares the element at that index with the target.
* If the element at mid is equal to the target, it returns mid.
* If the element at mid is less than the target, it means the target should be in the right half, so it updates low to mid + 1.
* If the element at mid is greater than the target, it means the target should be in the left half, so it updates high to mid - 1.
* The loop continues until low is greater than high.
* At this point, low is the position where the target should be inserted to maintain the sorted order.  

```java
class Solution {

    public int searchInsert(int[] nums, int target) {
        
        int start = 0;
        int end = nums.length - 1;

        while(start <= end) {
            int mid = start + (end - start)/2;

            if(nums[mid] == target) {
                return mid;
            } else if(nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return start;
    }
}
```

### Question 3

Problem Statement :- [**Find First and Last Position**](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

* here we have to also find the Occurrence of the target.
```java
public class FirstAndLastPosition {

    public static void main(String[] args) {
        int[] nums = new int[]{5, 7, 7, 8, 8, 9};
        int target = 8;
        int[] output = firstAndLastPosition( nums, target);
        System.out.println("The first and last index are :- " + output[0] + " , " + output[1]);
        int count = findOccurrenceOfTarget(nums, target);
        System.out.println("The Occurrence of target is :- " + count);
    }

    private static int findOccurrenceOfTarget(int[] nums, int target) {
        // this is sorted array so occurrence can be calculated by the last and first index
        return (lastOccurrence(nums, target) - firstOccurrence(nums, target)) + 1;
    }

    private static int[] firstAndLastPosition(int[] nums, int target) {

        int[] arr = new int[2];

        // To Find first occurrence
        arr[0] = firstOccurrence(nums, target);
        // To Find last occurrence
        arr[1] = lastOccurrence(nums, target);

        return arr;
    }

    public static int lastOccurrence(int[] nums, int target) {
        int ans = -1;

        int startIndex = 0;
        int endIndex = nums.length - 1;

        while(startIndex <= endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;

            if(nums[midIndex] == target) {
                ans = midIndex;
                //Here we are looking for the last occurrence, and obviously, we will find this  on right side of mid-value so updating
                startIndex = midIndex + 1;
            } else if(nums[midIndex] < target) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex - 1;
            }
        }
        return ans;
    }

    public static int firstOccurrence(int[] nums, int target) {
        int ans = -1;

        int startIndex = 0;
        int endIndex = nums.length - 1;

        while(startIndex <= endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;

            if(nums[midIndex] == target) {
                ans = midIndex;
                //Here we are looking for the first occurrence, and obviously, we will find this  on left side of mid-value so updating
                endIndex = midIndex - 1;
            } else if(nums[midIndex] < target) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex - 1;
            }
        }

        return ans;
    }
}
```

### Question 4

Problem Statement :- [**Pivot Element**](https://leetcode.com/problems/find-pivot-index/description/)
* A rotated and sorted array is one where elements are initially sorted in ascending order but have been rotated cyclically. For example, consider the array:

```java
public class FindPivotElement {

    public static void main(String[] args) {
        int[] array = new int[]{5, 6, 7, 0, 1, 2, 3, 4};
        int[] duplicateArray = new int[]{5, 6, 6, 7, 7, 7, 1, 1, 2, 3, 3, 4};
        int pivotElementForDuplicate = findPivotElementWithDuplicates(duplicateArray);
        // find the rotation count?
        int pivotElement = findPivotElement(array);
        System.out.println("The Pivot Element index is :- " + pivotElement);
        System.out.println("The Pivot Element from duplicate index is :- " + pivotElementForDuplicate);
    }

    /**
     * here, from the input we can figure out a few points
     * We have two-part of increasing arrays one is 5,6,7 and 0,1,2,3,4, so we have to find the 0 index value as output,
     * so we will calculate the mid-value first now we have to figure out in which part my mid-index exists
     * if it is in the second part then my pivot element will be mid or on the left side of mid, end = mid;
     * if it is in the first part then my pivot element will be in the right side start = mid + 1
     * so to check the part of the array we can check this condition arr[mid] > arr[0]
     * if the above condition is true that means it lying in the first part
     * if mid-part has existed in the second part then the above condition will never be true because it is rotated sorted array
     */
    public static int findPivotElement(int[] nums) {
        int startIndex = 0;
        int endIndex = nums.length - 1;
        //Here we are iterating till < because when start becomes y and end becomes y which is already calculated will
        // become infinite so removing =
        while(startIndex < endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;
            // checking the last element and first element greater to find the right side to search
            // if issue comes remove nums[midIndex] >= nums[nums.length-1]
            if(nums[midIndex] >= nums[nums.length - 1] && nums[midIndex] >= nums[0]) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex;
            }
        }

        return startIndex;
    }

    public static int findPivotElementWithDuplicates(int[] nums) {
        int startIndex = 0;
        int endIndex = nums.length - 1;
        //Here we are iterating till < because when start becomes y and end becomes y which is already calculated will
        // become infinite so removing =
        while(startIndex < endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;
            // checking the last element and first element greater to find the right side to search
            // if issue comes remove nums[midIndex] >= nums[nums.length-1]
            if(nums[midIndex] >= nums[nums.length - 1] && nums[midIndex] >= nums[0]) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex;
            }


             // So here, suppose we have a duplicate array so what do we have to do if we find duplicates we have to skip that
             //So how we can skip the duplicates by increasing the start and decreasing the end
             //But what if startIndex and endIndex itself are pivot elements so before that we will check the condition
            //If startIndex is the pivot element then the previous value will be greater than the current start index, we have to move towards the right to start++
            //If endIndex is the pivot element then the next value should be greater, and we have to move the left side so moving end --

            if(nums[midIndex] == nums[startIndex] && nums[midIndex] == nums[endIndex]) {
               
                if(nums[startIndex] < nums[startIndex - 1]) {
                    return startIndex;
                }

                startIndex++;

                if(nums[endIndex] < nums[endIndex + 1]) {
                    return endIndex - 1;
                }

                endIndex--;
            }
        }

        return startIndex;
    }
}
```

### Question 5
Problem Statement:-

**Given an ascending sorted rotated array arr of distinct integers of size N. The array is right-rotated K times. Your task is to find the value of K.** <br>
**Constraints** <br>
1 <= N <=10^5 <br>
1 <= arr[i] <= 10^7 <br>
**Sample Input** <br>
6 <br>
5 6 1 2 3 4 <br>
**Sample Output** <br>
2 <br>

**Solution** :-

**So here code will be the same as the pivot element but to find how many times it is rotated we have to get that pivot index and that only will be the count of rotation.**

### Question 6
Problem Statement:-

**Suppose an array of length n sorted in ascending order is rotated between 1 and n times. <br>
2. Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]]. <br>
3. Given the sorted rotated array nums of unique elements, return the minimum element of   this array. <br>
4. You must write an algorithm that runs in O(log n) time.** <br>
**Constraints** <br>
n == nums.length <br>
1 <= n <= 5000 <br>
-5000 <= nums[i] <= 5000 <br>
All the integers of numbers are unique. <br>
nums is sorted and rotated between 1 and n times. <br>
**Sample Input** <br>
6 <br>
5 6 1 2 3 4 <br>
**Sample Output** <br>
1

**Solution** :-

**Here also to find the minimum element so same pivot element logic we can use here.**

### Question 7
Problem Statement:-
**Given a sorted array containing only 0s and 1s, find the transition point. Transition Point is defined as 1's starting point. If there is no transition point, return -1.** <br>
**Constraints** <br>
1 <= N <= 500000 <br>
0 <= arr[i] <= 1 <br>
**Sample Input** <br>
6                <br>
0 0 0 0 1 1      <br>
**Sample Output** <br>
4

```java
import java.util.Scanner;

public class FindTransitionPoint {

    public static int findTransition(int[] arr) {
        int low = 0;
        int high = arr.length - 1;

        while (low < high) {

            int mid = (low + high) / 2;
            if(arr[mid] == 0) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        return low;
    }

    public static void main(String[]args) {

        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
         scanner.close();
        System.out.println(findTransition(arr));
    }
}
```

### Question 8 
Problem Statement:- 

**There is an integer array nums sorted in ascending order (with distinct values).nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2]. Given the array nums after the rotation and an integer target, return the index of the target if it is in nums, or -1 if it is not in nums. You must write an algorithm with O(log n) runtime complexity.**
**Constraints**<br>
1 <= nums.length <= 5000<br>
-10^4 <= nums[i] <= 10^4<br>
All values of numbers are unique.<br>
nums is guaranteed to be rotated at some pivot.<br>
-10^4 <= target <= 10^4<br>
**Sample Input**
7 <br>
4 5 6 7 0 1 2<br>
1 <br>
Sample Output <br>
5 <br>
Solution:- <br>

```java
public class SearchRotatedArray {

    public static void main(String[] args) {
        int[] array = new int[]{5, 6, 7, 0, 1, 2, 3, 4};
        int target = 0;
        int searchElement = search(array, target);
        System.out.println("The search Element index is :- " + searchElement);
    }

    /**
     * To search in a rotated array first we have to find the PIVOT element in this example {5, 6, 7, 0, 1, 2, 3, 4} pivot element is 0
     * and after finding the PIVOT element we can say that as the array is sorted and rotated so searching element will be lying in between
     * pivot to endIndex or pivot to startIndex, so after that, we can apply binary search easily.
     */
    private static int search(int[] nums, int target) {

        int pivotIndex = findPivotElement(nums);
        int startIndex = 0;
        int endIndex = nums.length - 1;

        if(target >= nums[pivotIndex] &&  target <= nums[nums.length - 1]) {
            startIndex = pivotIndex;
        } else {
            endIndex = pivotIndex - 1;
        }

        while (startIndex <= endIndex) {
            int midIndex = startIndex + (endIndex - startIndex) / 2;
            if(nums[midIndex] == target) {
                return midIndex;
            } else if(nums[midIndex] < target) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex - 1;
            }
        }
        return -1;
    }

    public static int findPivotElement(int[] nums) {
        int startIndex = 0;
        int endIndex = nums.length - 1;
        //Here we are iterating till < because when start becomes y and end becomes y which is already calculated will
        // become infinite so removing =
        while(startIndex < endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;
            // checking the last element and first element greater to find the right side to search
            // if issue comes remove nums[midIndex] >= nums[nums.length-1]
            if(nums[midIndex] >= nums[nums.length - 1] && nums[midIndex] >= nums[0]) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex;
            }
        }

        return startIndex;
    }
}
```

### Question 9

Problem Statement
**Given an array of integers. Find a peak element in it. An array element is a peak if it is NOT smaller than its neighbors. For corner elements, we need to consider only one neighbor.**<br>
**Example:**<br>
**Input**: array[]= {5, 10, 20, 15}<br>
**Output**: 20<br>
The element 20 has neighbors 10 and 15,<br>
Both of them are less than 20.<br>

**Input**: array[] = {10, 20, 15, 2, 23, 90, 67}<br>
**Output**: 20 or 90<br>
The element 20 has neighbors 10 and 15, <br>
both of them are less than 20, similarly, 90 has neighbors 23 and 67.<br>

**The following corner cases give a better idea about the problem.**
If the input array is sorted in a strictly increasing order, the last element is always a peak element. For example, 50 is the peak element in {10, 20, 30, 40, 50}.<br>
If the input array is sorted in a strictly decreasing order, the first element is always a peak element. 100 is the peak element in {100, 80, 60, 50, 20}.<br>
If all elements of the input array are the same, every element is a peak element.<br>

```java



import java.util.*;

public class PeakElement {
    public static int findPeakElement(ArrayList<Integer> arr) {
        int n = arr.size(); // Size of array

        // Edge cases:
        if (n == 1) return 0;
        if (arr.get(0) > arr.get(1)) return 0;
        if (arr.get(n - 1) > arr.get(n - 2)) return n - 1;

        int low = 1, high = n - 2;
        while (low <= high) {
            int mid = (low + high) / 2;

            // If arr[mid] is the peak:
            // If this condition is true for arr[mid], we can conclude arr[mid] is the peak element. We will return the index ‘mid’.

            if (arr.get(mid - 1) < arr.get(mid) && arr.get(mid) > arr.get(mid + 1))
                return mid;

            // If we are on the left:
            //This means we are in the left half and we should eliminate it as our peak element appears on the right.
            if (arr.get(mid) > arr.get(mid - 1)) low = mid + 1;

            // If we are in the right:
            // Or, arr[mid] is a common point:
            //We are in the right half and we should eliminate it as our peak element appears on the left.
            else high = mid - 1;
        }
        // Dummy return statement
        return -1;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr =
            new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 5, 1));
        int ans = findPeakElement(arr);
        System.out.println("The peak is at index: " + ans);
    }
}

```

### Question 10

Problem Statement

**Given an array of integers sorted in ascending order and a target value, find the element in the array that has minimum difference with the target value.** <br>
Example 1: Input: a[] = [2, 5, 10, 12, 15], target = 6 <br>
Output: 5<br>
Explanation: The difference between the target value '6' and '5' is the minimum.<br>
Example 2: Input: a[] = [2, 5, 10, 12, 15], target = 5 Output: 5 <br>
Example 3: Input: a[] = [2, 5, 10, 12, 15], target = 8 Output: 10 <br>
Example 4: Input: a[] = [2, 5, 10, 12, 15], target = 11 Output: 10 <br>
Example 5: Input: a[] = [2, 5, 10, 12, 15], target = 20 Output: 15 <br>

```java
public class MinimumDifference {

    public static void main(String[] args) {
        int[] arr = new int[]{1, 3, 8, 10, 15};
        int target = 12;
        int output = findMinimumDifference(arr, target);
        System.out.println(output);
    }

    //So always keep in mind minimum difference will be exact in the position where the target exists because it will be 0 at that point
    //If key does not exist then when the binary search loop breaks then startIndex and endIndex will be always the closest elements present in the array
    private static int findMinimumDifference(int[] sorted array, int target) {
        // array index starts from 0 and the end index will be one less than length;
        int startIndex = 0;
        int endIndex = sortedArray.length - 1;
        // to find the mid-value
        int midIndex = startIndex + (endIndex - startIndex) / 2;

        // continue till startIndex is <= endIndex
        while (startIndex <= endIndex) {
            //found in a middle element
            if(sortedArray[midIndex] == target) {
                return midIndex;
            } else if (sortedArray[midIndex] < target) {
                //If mid-element is < then increase min because it will be on right side
                startIndex = midIndex + 1;
            } else {
                //If mid-element is > then reduce max because it will be on left side
                endIndex = midIndex - 1;
            }

            midIndex = startIndex + (endIndex - startIndex) / 2;

        }
        int startIndexDiff = Math.abs(sortedArray[startIndex] - target);
        int endIndexDiff = Math.abs(sortedArray[endIndex] - target);

        return startIndexDiff < endIndexDiff ? startIndex : endIndex;
    }
}
```

### Question 11

Problem Statement

**Given an array that is sorted, but after sorting some elements are moved to either of the adjacent positions, i.e., arr[i] may be present at arr[i+1] or arr[i-1]. Write an efficient function to search an element in this array. The element arr[i] can only be swapped with either arr[i+1] or arr[i-1]. For example, consider the array {2, 3, 10, 4, 40}, 4 is moved to the next position and 10 is moved to the previous position.**<br>
**Example** :  <br>
**Input**: arr[] =  {10, 3, 40, 20, 50, 80, 70}, key = 40 <br>
**Output**: 2 <br>
Output is an index of 40 in given array <br>

**Input**: arr[] =  {10, 3, 40, 20, 50, 80, 70}, key = 90 <br>
**Output**: -1 <br>
-1 is returned to indicate the element is not present <br>

```java
public class NearlySortedArray {

    public static void main(String[] args) {
        int[] arr =new int[]{10, 5, 20, 30, 40};
        int target = 5;
        int output = searchInNearlySortedArray(arr, target);
        System.out.println(output);
    }

    //Nearly sorted means 10 30 20
    // so in a nearly sorted array, the value can be possible in + 1 or - 1 so searching accordingly
    // as we are checking + 1 and - 1 so adding + 2 and - 2 as it is already checked
    public static int searchInNearlySortedArray(int[] arr, int target) {

        int startIndex = 0;
        int endIndex = arr.length - 1;

        while(startIndex <= endIndex) {

            int midIndex = startIndex + (endIndex - startIndex) / 2;
            //
            if (arr[midIndex] == target) {
                return midIndex;
            } else if(midIndex - 1 > 0 && arr[midIndex - 1] == target) {
                return midIndex -1;
            } else if(midIndex + 1 < arr.length - 1 && arr[midIndex + 1] == target) {
                return midIndex + 1;
            } else if (target > arr[midIndex]) {
                startIndex = midIndex + 2;
            } else {
                endIndex = midIndex - 2;
            }
        }

        return -1;

    }

}
```
### Question 12
Problem Statement

**Given a boolean 2D array, where each row is sorted. Find the row with the maximum number of 1s.**
**Constraints** <br>
1 <= n, m <= 40 <br>
0 <= mat[][] <=  <br>
**Sample** **Input** <br>
4 3 <br>
0 1 1 <br>
0 0 1 <br>
1 1 1 <br>
0 0 1 <br>
**Sample** **Output** <br>
2
```java
import java.util.Scanner;

public class MaximumNumberOf1Row {

    public static int findRow(int[][] arr) {

        int max = Integer.MIN_VALUE;
        int answer = -1;
        int count = 0;

        for (int i = 0; i < arr.length; i++) {
            int output = findTransition(arr[i]);
            int data = arr[i].length - output;
            count += data;
            if(data > max) {
                answer = i;
                max = data ;
            }
        }
        System.out.println("The maximum number of one in row is :- " + max);
        System.out.println("The total number of one in each row is :- " + count);
        return answer;
    }

    public static int findTransition(int[] arr) {
        int low = 0;
        int high = arr.length - 1;

        while (low < high) {

            int mid = (low + high) / 2;
            if(arr[mid] == 0) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        return low;
    }


    public static void main(String[]args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int m = scanner.nextInt();

        int[][] mat = new int[n][m];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                mat[i][j] = scanner.nextInt();
            }
        }
        scanner.close();
        System.out.println(findRow(mat));
    }
}
```

### Question 13
Problem Statement:- [**Check If N and its double Exist**](https://leetcode.com/problems/check-if-n-and-its-double-exist/description/)

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

//1346
public class CheckIfNAndItsDoubleExist {

    public static void main(String[] args) {
        checkIfExist(new int[]{});
        checkIfExistSet(new int[]{});
    }

    public static boolean checkIfExist(int[] arr) {
        // sorting the array for applying binary search
        Arrays.sort(arr);

        boolean result;

        for(int i = 0; i < arr.length; i++) {
            /** If the current index value is negative then the condition will be  value % 2 == 0, and if it is < 0 then its division by 2 can be there, how? why checking mod we want two multiple and 2 multiple is always even lets take one example
             -20, -10, -8, 15, 12 so here is what will happen -20 will come first
             then if -20 mod 2 == 0 and -20 < 0 , then only we will get it the arr[j] in upcoming indexes which will made the arr[i] = 2*arr[j]
             why because for negate sorted order bigger one comes first and then the smaller negative so if arr[i] == -20 then we have to look for 
             -10 in upcoming and if it is 20 then we will look for 40
             
            ------
             otherwise, if it is positive then its double will be there in upcoming indexes. because the array is sorted.**/
            if(arr[i] % 2 == 0 && arr[i] < 0) {
                result = binarySearch(arr, i + 1, arr.length - 1, arr[i]/2);
            } else {
                result = binarySearch(arr, i + 1, arr.length - 1, arr[i]*2);
            }

            if(result) return true;
        }

        return false;
    }

    private static boolean binarySearch(int[] arr, int start, int end, int target) {

        while(start <= end) {
            int mid = (start + end) / 2;

            if(arr[mid] == target) {
                return true;
            } else if (arr[mid] > target) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }

        return false;
    }

    public static boolean checkIfExistSet(int[] arr) {

        Set<Integer> checkSet = new HashSet<>();

        for (int element : arr) {

            int data = element % 2 == 0 ? element / 2 : -1;

            if ((checkSet.contains(element * 2)) || (checkSet.contains(element / 2) && data != -1)) {

                return true;
            } else {

                checkSet.add(element);
            }
        }

        return false;
    }
}
```

### Question 14
Problem Statement:- [**Valid Perfect Square**](https://leetcode.com/problems/valid-perfect-square/description/)

```java
class Solution {

    public boolean isPerfectSquare(int num) {
        
        int start = 1;
        int end = 46340;

        if (num == 1) return true;

        while (start <= end) {

            int mid = start + (end - start) / 2;

            if (mid * mid == num) {
                return true;
            } else if (mid * mid < num) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return false;
    }
}
```

# Medium Level Binary Search Questions

### Question 1
Problem Statement:-

**Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The results should also be sorted in ascending order. An integer a is closer to x than an integer b if:**<br>
       |a - x| < |b - x|, or<br>
       |a - x| == |b - x| and a < b<br>
**Constraints** <br>
1 <= k <= arr.length <br>
1 <= arr.length <= 10^4 <br>
arr is sorted in ascending order. <br>
-10^4 <= arr[i], x <= 10^4 <br>
**Sample Input** <br>
6 <br>
10 20 30 40 50 60 <br>
3 <br>
45 <br>
**Sample Output** <br>
30 40 50 <br>

**Solution**:- 

```java
import java.util.ArrayList;
import java.util.Collections;

public class FindKthClosestElement {

    public static void main(String[] args) {
        int[] arr = new int[]{10,20,30,40,50};
        int target = 45;
        int k = 3;
        ArrayList<Integer> output = findKthClosestElement(arr, k, target);
        output.forEach(System.out::println);

    }

    /**
     * Here we have to find the kth closest element we have given a K ex. 3 and the target is 45
     * for the array = [10,20,30,40,50] so we have to find 3 closest elements to 45
     * so, we will apply binary search to reach the closest position of the target and
     * then we have startIndex and endIndex and we will try to find kth closest element
     * so for that we should have to take two pointers left and right,
     * 
     * so left we will assign it to endIndex and right we will assign it to startIndex
     * why? because binary search breaks when endIndex crosses startIndex so the end will be the left side and 
     * start will be the right side.
     * 
     * and we have to handle some corner cases like 
     * if left crosses 0 index and right crosses out of length index
     * and k > 0 so till then loop will continue and,
     * we will take the difference and in the output list we will add the smaller value and move the pointer accordingly
     * 
     * and suppose one case if left crosses 0 index but k is still > 0 then we have to add all right side element
     * right?
     * and similarly vice-versa
     * @param arr
     * @param k
     * @param target
     * @return
     */
    private static ArrayList<Integer> findKthClosestElement(int[] arr, int k, int target) {

        int length = arr.length;
        int startIndex = 0;
        int endIndex = length - 1;
        int midIndex = 0;

        while(startIndex <= endIndex) {

            midIndex = startIndex + (endIndex - startIndex) / 2;

            if(arr[midIndex] == target) {
                break;
            } else if (arr[midIndex] < target) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex - 1;
            }
        }

        ArrayList<Integer> result = new ArrayList<>();

        // e = 3, s = 4 // if issue comes then left = midIndex - 1, right = midIndex
        int left = endIndex;
        int right = startIndex;

        while (left >= 0 && right < length && k > 0) {

            if(Math.abs(arr[left] - target) <= Math.abs(arr[right] - target)) {
                result.add(arr[left]);
                left--;
            } else {
                result.add(arr[right]);
                right++;
            }
            k--;
        }

        while (k > 0 && left >= 0) {
            result.add(arr[left]);
            left--;
            k--;
        }

        while (k > 0 && right < length) {
            result.add(arr[right]);
            right++;
            k--;
        }


        Collections.sort(result);

        return result;
    }
}

```
### Question 2
Problem Statement:-

**Given a sorted array arr[] of size N. Find the element that appears only once in the array. All other elements appear exactly twice.** <br>
**Constraints** -> O(1), O(logN) <br>
10^5 <= N <= 10^5 <br>
**Sample Input** <br>
11 <br>
1 1 2 2 4 4 7 7 8 10 10 <br>
**Sample Output** <br>
8

```java
public class FindElementAppearsOne {

    public static void main(String[] args) {
        // 11,22,22,34,34,57,57
        // 1 1 2 2 4 4 7 7 8 10 10
        int[] arr = new int[]{1,1,2,3,3,4,4,8,8};
        System.out.println(findElementAppearsOne(arr));
    }

    /**
     *
     */
    private static Integer findElementAppearsOne(int[] a) {

        // handling corner cases
        if(a.length == 0) return -1;
        else if(a.length == 1) return a[0];

        //corner cases where a unique element will be at the start or end
        if(a[0] != a[1]) {
            return a[0];
        }
        if(a[a.length-1] != a[a.length-2]){
            return a[a.length-1];
        }

        int l=0;
        int h = a.length-1;

        while(l <= h){
            int m = (l + h) / 2;

            //when a unique element is in between
            if(a[m] != a[m-1] && a[m] != a[m+1]){
                return a[m];
            }
            //if the unique element is not crossed,
            //a 'm' is odd, then prev element will always be the same
            //b 'm' is even, then the next element will always be the same
            if((m % 2 == 1 && a[m] == a[m-1]) || (m % 2 == 0 && a[m] == a[m+1])){
                l = m + 1;
            }else{
                h = m - 1;
            }
        }
        //if all elements occur twice
        return -1;
    }
}
```

### Question 3
Problem Statement:-

**Given a sorted array of size N. Count the number of distinct absolute values present in the array.** <br>
**Constraints** <br>
1 <= N <= 10^5 <br>
-10^8 <= Arr[i] <= 10^8 <br>
The array may contain duplicates <br>
**Sample Input** <br>
6  <br>
-3 -2 0 3 4 5 <br>
**Sample Output** <br>
5 <br>

```java

```
