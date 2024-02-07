---
layout: post
title: Binary Search 👋
date: 2024-01-12 03:00:00 +0900
description: Binary Search Implementation
categories: [Data Structures and Algorithms]
tags: [blog, coding, computer-science , notes, computer, data-structures-and-algorithms-for-coding-interview, data-structures,algorithms, interview, coding-interview, dsalgo, leetcode, gfg, geeksforgeeks, dsa, binary-search]
math: false
mermaid: false
---

# Problem 1: Binary Search Algorithm

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
Problem Statement :-
**You are given an array ‘pages’ of integer numbers. In this array, the ‘pages[i]’ represents the number of pages in the ‘i-th’ book. There are ‘m’ number of students, and the task is to allocate all the books to the students.** 

Allocate books in a way such that:

Each student gets at least one book. <br>
Each book should be allocated to a student. <br>
Book allocation should be in a contiguous manner. <br>
 
You have to allocate the books to ‘m’ students such that the maximum number of pages assigned to a student is minimum.

**Input** <br>
Number of books = 4 and Number of students = 2

pages[] = { 10,20,30,40}

**Output** <br>
60

**Brute Force**
```java
import java.util.Arrays;
import java.util.Scanner;

public class BookAllocation {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int[] arr = new int[scan.nextInt()];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = scan.nextInt();
        }
        int m = scan.nextInt();

        System.out.println(findPages(arr, m));


        scan.close();
    }

    public static int findPages(int[] arr, int m) {
        if (m > arr.length) {
            return -1;
        }

        int low = Arrays.stream(arr).max().getAsInt();
        int high = Arrays.stream(arr).sum();
        for (int i = low; i <= high; i++) {
            if (countStudents(arr, i) == m) {
                return i;
            }
        }


        return low;


    }

    private static int countStudents(int[] arr, int i) {
        int sum = 0;
        int student = 1;
        for (int j = 0; j < arr.length; j++) {
            if (sum + arr[j] <= i) {
                sum += arr[j];
            } else {
                student++;
                sum = arr[j];
            }
        }
        return student;
    }

}
```

**Optimal Approach**
```java
import java.util.Arrays;
import java.util.OptionalInt;

//https://www.codingninjas.com/codestudio/problem-details/allocate-books_1090540
//https://www.codingninjas.com/codestudio/problems/painter-s-partition-problem_1089557
public class BookAllocationProblem {

    public static void main(String[] args) {
        int[] arr = new int[]{1, 2, 3, 4};
        int numberOfStudent = 2;
        // boolean status = isPossibleSolution(arr, 75, numberOfStudent);
        int output = bookPartition(arr, numberOfStudent);
        System.out.println("The Output is :- " + output);
    }

    private static int bookPartition(int[] arr, int numberOfStudent) {
        // here possible output can be min value from array if arr.length == number of student,
        // but it is not sorted so taking 0
        int startIndex = 0;
        // here possible output can be sum of all value from array if arr.length == 1 student,
        int endIndex = Arrays.stream(arr).sum();
        //output int output = -1;
        // handling corner case
        if(arr.length == numberOfStudent) {
            OptionalInt maxValue = Arrays.stream(arr).max();
            if(maxValue.isPresent()) {
                return maxValue.getAsInt();
            }
        } else if(numberOfStudent == 1) {
            return endIndex;
        }
        // we created search space for binary search from startIndex to endIndex
        while (startIndex <= endIndex) {
            // getting mid-index to find the solution
            int midIndex = startIndex + (endIndex - startIndex) / 2;

            if(isPossibleSolution(arr, midIndex, numberOfStudent)) {
                //output = midIndex;
                // if midIndex is possible solution then output must be lesser than the midIndex
                endIndex = midIndex - 1;
            } else {
                // if midIndex is not possible solution then output must be greater than the midIndex
                startIndex = midIndex + 1;
            }
        }
        // return output;
        return startIndex;
    }

    private static boolean isPossibleSolution(int[] arr, int midIndex, int numberOfStudent) {

        int student = numberOfStudent;
        int index = 0;
        int sum = 0;
        // here checking index must be less than length
        while (index < arr.length) {
            // sum of array element
            sum = sum + arr[index];
            if(sum > midIndex) {
                // find the first partition for the student
                sum = 0;
                student -= 1;
            } else {
                index++;
            }
           // checking if the partition completed among student still we have book left
            // here when arr element itself is greater than midIndex value than obviously it will be false
            if(student == 0 && index < arr.length) {
                return false;
            }
        }

        return true;
    }
}
/**
 *         int studentCount = 1;
 *         int pageSum = 0;
 *
 *         for (int element : arr) {
 *             if (pageSum + element > midIndex) {
 *                 pageSum = pageSum + element;
 *             } else {
 *                 studentCount++;
 *                 if (studentCount > numberOfStudent || element > midIndex) {
 *                     return false;
 *                 }
 *                 pageSum = element;
 *             }
 *         }
 */
```

### Question 4
Problem Statement :-

**Given an array/list of length ‘n’, where the array/list represents the boards and each element of the given array/list represents the length of each board. Some ‘k’ numbers of painters are available to paint these boards. Consider that each unit of a board takes 1 unit of time to paint.**

**You are supposed to return the area of the minimum time to get this job done of painting all the ‘n’ boards under a constraint that any painter will only paint the continuous sections of boards.**

**Example** : <br>
Input: arr = [2, 1, 5, 6, 2, 3], k = 2

**Output**: 11

**Explanation**: <br>
**First painter can paint boards 1 to 3 in 8 units of time and the second painter can paint boards 4-6 in 11 units of time. Thus both painters will paint all the boards in max(8,11) = 11 units of time. It can be shown that all the boards can't be painted in less than 11 units of time.**

**Solution**:-
The Solution is similar to Book Allocation Algorithm.

### Question 5:-
Problem Statement :-

**Lumberjack Mirko needs to chop down M metres of wood. It is an easy job for him since he has a nifty new woodcutting machine that can take down forests like wildfire. However, Mirko is only allowed to cut a single row of trees.**

**Mirko‟s machine works as follows: Mirko sets a height parameter H (in metres), and the machine raises a giant sawblade to that height and cuts off all tree parts higher than H (of course, trees not higher than H meters remain intact). Mirko then takes the parts that were cut off. For example, if the tree row contains trees with heights of 20, 15, 10, and 17 metres, and Mirko raises his sawblade to 15 metres, the remaining tree heights after cutting will be 15, 15, 10, and 15 metres, respectively, while Mirko will take 5 metres off the first tree and 2 metres off the fourth tree (7 metres of wood in total).**

**Mirko is ecologically minded, so he doesn‟t want to cut off more wood than necessary. That‟s why he wants to set his sawblade as high as possible. Help Mirko find the maximum integer height of the sawblade that still allows him to cut off at least M metres of wood.**

**Input** <br>
**The first line of input contains two space-separated positive integers, N (the number of trees, 1 ≤ N ≤ 1 000 000) and M (Mirko‟s required wood amount, 1 ≤ M ≤ 2 000 000 000).**

**The second line of input contains N space-separated positive integers less than 1 000 000 000, the heights of each tree (in metres). The sum of all heights will exceed M, thus Mirko will always be able to obtain the required amount of wood.**

**Output** <br>
The first and only line of output must contain the required height setting.

**Example** <br>
**Input**: <br>
4 7 <br>
20 15 10 17 <br>
**Output**: <br>
15 <br>

**Input**: <br>
5  20 <br>
4 42 40 26 46 <br>
**Output**: <br>
36

```java
import java.util.Arrays;
import java.util.OptionalInt;

public class SPOJEKOProblem {

    public static void main(String[] args) {

        int[] nums = new int[]{4, 42, 40, 26, 46};
        int target = 20;
        int output = ekoProblem( nums, target);
        System.out.println("The output is :- " + output);

    }

    private static int ekoProblem(int[] nums, int target) {
        int startIndex = 0;
        int endIndex = 0;
        OptionalInt maxValue = Arrays.stream(nums).max();
        if(maxValue.isPresent()) {
            endIndex = maxValue.getAsInt();
        }

        while (startIndex <= endIndex) {
            int midIndex = startIndex + (endIndex - startIndex) / 2;
            int returnValue = isPossibleSolution(nums, midIndex);
            if(returnValue == target) {
                return midIndex;
            } else if(returnValue > target) {
                startIndex = midIndex + 1;
            } else {
                endIndex = midIndex - 1;
            }
        }
        return startIndex;
    }

    private static int isPossibleSolution(int[] nums, int midIndex) {

        int sum = 0;

        for(int data : nums) {
            if (data >= midIndex) {
                sum += (data - midIndex);
            }
        }
        return sum;
    }
}
```
### Question 6
Problem Statement :-

Problem statement
You are given an array 'arr' consisting of 'n' integers which denote the position of a stall.

You are also given an integer 'k' which denotes the number of aggressive cows.

You are given the task of assigning stalls to 'k' cows such that the minimum distance between any two of them is the maximum possible.

Print the maximum possible minimum distance.

Example: <br>
Input: 'n' = 3, 'k' = 2 and 'arr' = {1, 2, 3}
Output: 2

Explanation: The maximum possible minimum distance will be 2 when 2 cows are placed at positions {1, 3}. Here distance between cows is 2.
Detailed explanation ( Input/output format, Notes, Images )

Sample Input 1 : <br>
6 4 <br>
0 3 4 7 10 9 <br>
Sample Output 1 : <br>
3

Explanation to Sample Input 1 :
The maximum possible minimum distance between any two cows will be 3 when 4 cows are placed at positions {0, 3, 7, 10}. Here distance between cows are 3, 4 and 3 respectively.

Sample Input 2 : <br>
5 2 <br>
4 2 1 3 6 <br>

Sample Output 2 : <br>
5 <br>

Expected time complexity:
Can you solve this in O(n * log(n)) time complexity?


Constraints : <br>
2 <= 'n' <= 10 ^ 5 <br>
2 <= 'k' <= n <br>
0 <= 'arr[i]' <= 10 ^ 9 <br>
Time Limit: 1 sec. <br>

```java
import java.util.Arrays;

public class AggressiveCowsProblem {

    public static void main(String[] args) {

        int[] arr = new int[]{4,2,1,3,6};
        int numberOfCows = 2;
        int output = aggressiveCows(arr, numberOfCows);
        System.out.println("The Output is :- " + output);
    }

    private static int aggressiveCows(int[] arr, int numberOfCows) {
        Arrays.sort(arr);
        // this is min value of search space
        int startIndex = 0;
        int endIndex =  arr[arr.length - 1];

        // output
        int output = -1;

        while(startIndex <= endIndex) {
            int midIndex = startIndex + (endIndex - startIndex) / 2;
            // if it is a possible solution then for finding longest we will go right side
            // because there is a chance we will find minimum distance as large as possible
            if(isPossibleSolution(arr, midIndex, numberOfCows)) {
                output = midIndex;
                startIndex = midIndex + 1;
            } else {
                // if this is not a possible solution then that right side element will also not be possible solution
                // so moving left side to find solution
                endIndex = midIndex - 1;
            }
        }

        return output;
    }

    private static boolean isPossibleSolution(int[] arr, int midIndex, int numberOfCows) {
        // here starting point will be 0 always
        int startPoint = arr[0];
        // maintain counter to check number of cows assigned
        int counter = 1;
        for(int i = 1; i < arr.length; i++) {
            // considering midIndex as max distance
            // if diff of arr[i] - start point >= midIndex that means we got one position for cow for considered maximum distance as midIndex
            // once we got distance C2 got placed then we will search place for C3, so we have to update the start point to C2 position
            // and after that if we find the position for C3 also it's a possible solution else return false
            if(Math.abs(arr[i] - startPoint) >= midIndex) {
                        counter++;
                        startPoint = arr[i];
            }
            if(counter == numberOfCows) return true;
        }

        return false;
    }

}
```

### Question 7
Problem Statement :-

Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.

Example 1:

Input: piles = [3,6,7,11], h = 8 <br>
Output: 4 <br>

Example 2:

Input: piles = [30,11,23,4,20], h = 5 <br>
Output: 30 <br>

Example 3:

Input: piles = [30,11,23,4,20], h = 6 <br>
Output: 23 <br>
 
Constraints: <br>
1 <= piles.length <= 104 <br>
piles.length <= h <= 109 <br>
1 <= piles[i] <= 109 <br>

```java
import java.util.Arrays;

public class EatingBanana {

    /**
     * 3     6      7      11
     * 8
     * low -> 1 , high -> 11 , mid -> 6
     * isPossible -> 6
     * 3 6 7 11
     * 1 1 2 2 -> 6h <= 8h possible solution return true;
     */
    public static void main(String[] args) {
        int[] arr = new int[]{3, 6, 7, 11};
        int hours = 8;
        System.out.println(getMinimumRate(arr, hours));
    }

    private static Integer getMinimumRate(int[] arr, int hours) {
        Arrays.sort(arr);
        int low = arr[0];
        int high = arr[arr.length - 1];

        while (low <= high) {

            int mid = (low + high) / 2;

            if(isPossibleSolution(arr, hours, mid)) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }

        }
        return low;
    }

    /**
     * 3 6 7 11
     * 1 1 2 2 -> 6h <= 8h possible solution return true;
     */
    private static boolean isPossibleSolution(int[] arr, int hours, int mid) {
        // speed = 0;
        int speed = 0;

        for(int data : arr) {
            // if 3 / 6 , 6 / 6, ..... here if mid will be less than mid-element then speed becomes 0, and he will be able to eat in 1h -> so if we are getting 0 then checking condition and increasing speed
            //                         here if mid will be more than mid-element then speed becomes like 11 / 4 -> 2
            //                         here if mid will be equal to mid-element then speed becomes like 7/7 -> 1 so next if condition will break
            speed += data / mid; // ->

            if(data % mid != 0) speed++;
        }

        //if speed is less than the given h hours, We need to increase Speed,to increase speed we need to select lower value between low ---- > mid-1 as mid;
        return speed <= hours;
    }

    /**
     * for easy understanding solution
    private static boolean isPossibleSolutionUpdated(int[] arr, int hours, int mid) {

        int totalH = 0;

        for (int i = 0; i < arr.length; i++) {
            totalH += Math.ceil((double)(arr[i]) / (double)(hours));
        }

        //if speed is less than the given h hours, We need to increase Speed,to increase speed we need to select lower value between low ---- > mid-1 as mid;
        return totalH <= hours;
    }
     **/
}

```

### Question 8

Problem Statement:- [**Heaters**](https://leetcode.com/problems/heaters/description/)

```java
public class Heaters {

    /**
     * Winter is coming! During the contest, your first job is to design a standard heater with a fixed warm radius to warm all the houses.
     * 2. Every house can be warmed, as long as the house is within the heater's warm radius range.
     * 3. Given the positions of houses and heaters on a horizontal line, return the minimum radius standard of heaters so that those heaters could cover all houses.
     * 4. Notice that all the heaters follow your radius standard, and the warm radius will be the same.
     * Constraints
     * 1 <= houses.length, heaters.length <= 3 * 10^4
     * 1 <= houses[i], heaters[i] <= 10^9
     * Sample Input
     * 4
     * 1 2 5 7
     * 2
     * 1 4
     * Output
     * 1 2 5 7
     * (min (1-1, 4 - 1) -> 0) similarly ->  1 1 3
     * 1 4
     * 3
     *
     */
    public static void main(String[] args) {

        int houseCount = 4;
        int heaterCount = 2;
        int[] house = new int[]{1, 2, 5, 7};
        int[] heater = new int[]{1, 4};

       System.out.println(getMaxRadiusOfHeater(house, houseCount, heater, heaterCount));
    }

    private static Integer getMaxRadiusOfHeater(int[] house, int houseCount, int[] heater, int heaterCount) {
        // to capture maximum distance required
        int maxRadius = 0;

        for(int i = 0; i < houseCount; i++) {
            // we will consider the minimum distance between nearest two heaters
            int output = getNearestHeaterRadius(house[i], heater, heaterCount);
            // return maximum
            maxRadius = Math.max(maxRadius, output);
        }

        return maxRadius;
    }

    private static int getNearestHeaterRadius(int data, int[] heater, int heaterCount) {
        int low = 0;
        int high = heaterCount - 1;
        int upper = 0;
        int lower = 0;
        while (low <= high) {
            int mid = (low + high) / 2;
            if(heater[mid] == data) {
                return 0;
            } else if(heater[mid] < data) {
                lower = mid;
                low = mid + 1;
            } else {
                upper = mid;
                high = mid - 1;
            }
        }

        return Math.min(Math.abs(data - heater[lower]), Math.abs(data - heater[upper]));
    }
}
```

### Question 9

**Given an array of integer numbers and an integer threshold, we will choose a positive integer divisor, divide all the array by it, and sum the division's result. Find the smallest divisor such that the result mentioned above is less than or equal to threshold.**

**Each result of the division is rounded to the nearest integer greater than or equal to that element. (For example: 7/3 = 3 and 10/2 = 5).**

**It is guaranteed that there will be an answer**

Constraints

1 <= nums.length <= 5 * 10^4 <br>
1 <= nums[i] <= 10^6 <br>
nums.length <= threshold <= 10^6 <br>
Sample Input <br>
4 <br>
1 2 5 9 <br>
6 <br>
Sample Output <br>
5 <br>
Solution:-  <br>
**Solution is same as koko eating Banana please try by yourself***

### Question 9

1. A conveyor belt has packages that must be shipped from one port to another within D days.

2. The ith package on the conveyor belt has a weight of weights[i]. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.

3. Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within D days.

Constraints <br>
1 <= days <= weights.length <= 5 * 10^4 <br>
1 <= weights[i] <= 500 <br>
Sample Input <br>
10 <br>
2 3 4 1 5 6 7 9 8 10 <br>
5 <br>
Sample Output <br>
15 <br>


```java
public class ShipPackages {

    public static void main(String[] args) {
        // Sample input
        int[] weights = {2, 3, 4, 1, 5, 6, 7, 9, 8, 10};
        int days = 5;

        // Calling the shipWithinDays function and printing the result
        int result = shipWithinDays(weights, days);
        System.out.println(result);
    }

    // Function to find the least weight capacity of the ship
    public static int shipWithinDays(int[] weights, int days) {
        // Set the initial search space
        int left = 1;
        int right = 500 * weights.length; // Maximum weight capacity

        // Perform binary search
        while (left < right) {
            // Calculate the middle point
            int mid = left + (right - left) / 2;

            // Check if the current capacity is sufficient
            if (canShipWithinDays(weights, days, mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        // The left pointer now contains the minimum weight capacity
        return left;
    }

    // Function to check if all packages can be shipped within the specified days with given capacity
    private static boolean canShipWithinDays(int[] weights, int days, int capacity) {
        int currentCapacity = 0;
        int requiredDays = 1;

        // Iterate through the weights array
        for (int weight : weights) {
            // If adding the current weight exceeds the capacity, reset currentCapacity and increase requiredDays
            if (currentCapacity + weight > capacity) {
                currentCapacity = 0;
                requiredDays++;
            }
            
            // Add the current weight to the currentCapacity
            currentCapacity += weight;
        }

        // Check if the required days are less than or equal to the specified days
        return requiredDays <= days;
    }
}
```

