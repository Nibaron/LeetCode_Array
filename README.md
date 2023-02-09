# Array-101

Arrays are a simple data structure for storing lots of similar items. They exist in all programming languages, and are used as the basis for most other data structures. On their own, Arrays can be used to solve many interesting problems. Arrays come up very often in interview problems, and so being a guru with them is a must!

**Task #1**
## Max Consecutive Ones
> Sample Input Output
```
Given a binary array nums, return the maximum number of consecutive 1's in the array
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

```
> My Code
```
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int res=0,count=0;
        for(int i=0; i<nums.size(); i++)
        {
            if(nums[i]==1)
            {
                count++;
            }
            
            if(nums[i]!=1)
            {
                count=0;
            }
            
            if(count>res)
                res=count;      
    }
        return res;
    }
};
```
>Best Code
```
 int findMaxConsecutiveOnes(vector<int>& nums) {
        int max_cnt = 0, cnt = 0;
        for (auto n : nums) {
            if (n == 1) max_cnt = max(++cnt, max_cnt);
            else cnt = 0;
        }
        return max_cnt;
    }
```
**Task #2**
## Find Numbers with Even Number of Digits
> Sample Input Output
```
Given an array `nums` of integers, return how many of them contain an even number of digits.
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 12-> 2 digits, 345-> 3 digits, 2,6-> 1 digit, 7896-> 4 digits.

```
> My Approach

```
Use a function called `digit` to calculate digit of any number.
Then we call this function for each numbers in the array and count the even numbers.

```
> My Code
```
class Solution {
public:
    int digit(int num)
    {
        int flag=0;
        while(num>0)
        {
            num=num/10;
            flag++;
        }
        return flag;
    }
    
    int findNumbers(vector<int>& nums) {
        int count=0;
        for(int i=0; i<nums.size();i++)
        {
            int check=digit(nums[i]);
            
            if(check%2==0)
                count++;
                
        }
        return count;
    }
};
```
> Approach 2

We can calculate digits using logarithm function.
`((int(log10(num)+1)) % 2) == 0`

>Code
```
#include<math.h>
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int count=0;
        for(auto const num : nums){
            if(((int(log10(num)+1)) % 2) == 0){
            count++;
            }
        }
        return count;
    }
};
```
>Approach 3

Only numbers between 10 and 99 or 1000 and 9999 or 100000 have even number of digits.

1-9 > odd

10-99 > even

100-999 > odd

1000-9999 > even

10000 - 99999 > odd

100000= even

Taking advantage of `nums[i] <= 10^5` (given Constrain)

>Code
```
class Solution {
public:
    int findNumbers(vector<int>& nums) {
        int n,count=0;
        for(int i=0;i<nums.size();i++)
        {
            n=nums[i];
            if(( 10<=n && n<=99) || (1000<=n && n<=9999 ) || ( n==100000 ))
            {
               count++;
            }
        }
        return count;
    }
};
```
>Approach 4

Convert the number to string. Using `string.length()`, we can find the length.
If it is even , increment the count.

>Code
```
class Solution {
public:
    int findNumbers(vector<int>& nums) {
    int count=0;
    for(auto e : nums) 
        if(to_string(e).length()%2==0) count++;

    return count;
    }
}
```
**Task #3**
## Squares of a Sorted Array
> Sample Input Output
```
Given an integer array nums sorted in non-decreasing order, 
return an array of the squares of each number sorted in non-decreasing order.
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].

After sorting, it becomes [0,1,9,16,100].

```
> My Approach

```
First, square every number with i*i, if any negative, then make it positive,
Then Sort the array.

```
> My Code
```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for(int i=0; i<nums.size(); i++)
        {
            nums[i]=nums[i]*nums[i];
            
            if(nums[i]<0)
                nums[i]=nums[i]*(-1);
        }
        
        sort(nums.begin(),nums.end());
        return nums;
    }
};
```


**Task #4**
## Duplicate Zeros
> Sample Input Output
```
Given a fixed-length integer array `arr`, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written. 

Do the above modifications to the input array in place and do not return anything.

Input: [1,0,2,3,0,4,5,0]
Output: [1,0,0,2,3,0,0,4]
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]

if any `0` found, do a `left shift` operation.

```
> My Approach

```
Take another vector, push values, if 0 found,
push another 0 too. Do it until nums.size().

REMEMBER, if we don't use another vector, then we have to use nested loop.
Then, complexity O(n^2).
My code has O(n).

```
> My Code
```
class Solution {
public:
    void duplicateZeros(vector<int>& arr) {
        vector <int> nums;
        for(int i=0; i<arr.size(); i++)
        {
            nums.push_back(arr[i]);
            
            if(arr[i]==0)
                nums.push_back(0);
        }
        for(int i=0; i<arr.size(); i++)
        {
            arr[i]=nums[i];
        }
    }
};
```
**Task #5**
## Remove Element
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

`Do not allocate extra space for another array`. You must do this by `modifying the input array` in-place with `O(1)` extra memory.

> Sample Input Output
```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```
> My Approach

If the element `val` found, erase it with erase function.

> My Code
```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int flag=0, sz=nums.size();
        for(int i=0; i<nums.size(); i++){
            if(nums[i]==val){
                flag++;
                nums.erase(nums.begin()+i);
                i--;
            }
        }
        return sz-flag;
    }
};
```
> Approach 2 `two pointer approach`

The solution uses two pointers, `i` and `j`, to traverse the vector `nums`. 
The pointer `i` is used to iterate over `all elements` of the vector, 
while the pointer `j` is used to keep track of the position of the `next non-val` element in the modified vector.

> Code
```
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
    
    int j=0;
    for(int i=0;i<nums.size();i++){
        if(nums[i]!=val)
        {
            nums[j]=nums[i];
            j++;
        }
    }
    return j;
    }
};
```

**Task#6**
## Remove Duplicates from Sorted Array

> Approach  `two pointer approach`

> My Code
```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
     if(nums.size()==0)
         return 0;
    int len=1;
    for(int i=1; i<nums.size(); i++)
    {
        if(nums[i]!=nums[i-1])
        {
            nums[len]=nums[i];
            len++;
        }
    }
        return len;
    }
};
```

**Task#7**
 ## Check If N and Its Double Exist
 
 > Sample Input Output
```
Input: arr = [10,2,5,3]
Output: true
Explanation: For i = 0 and j = 2, arr[i] == 10 == 2 * 5 == 2 * arr[j]
Input: arr = [3,1,7,11]
Output: false
Explanation: There is no i and j that satisfy the conditions.
```
> My Approach


We can solve it using nested loop.

> My Code
```
class Solution {
public:
    bool checkIfExist(vector<int>& arr) {
        
        for(int i=0; i<arr.size(); i++)
        {
           for(int j=0; j<arr.size(); j++) 
           {
               if(i != j && arr[i]==2*arr[j])
                   return true;
           }
        }
        return false;
    }
};
```

> Approach 2
```
We can solve it using the set function.
1. First, create a set.
2. For a value n, find 2*n or if n is even , find n/2.
```

> Code

```
class Solution {
public:
    bool checkIfExist(vector<int>& arr) {
        unordered_set<int> set;
        for(int i=0;i<arr.size();i++){
            if(set.count(2*arr[i])>0 || ((arr[i]%2==0) && set.count(arr[i]/2)>0))
                return true;
            set.insert(arr[i]);
        }
        return false;
    }
};
```
**Task #8 **
## Valid Mountain Array

https://leetcode.com/explore/learn/card/fun-with-arrays/527/searching-for-items-in-an-array/3251/
 
 > Sample Input Output
```
Input: arr = [0,3,2,1]
Output: true

Input: arr = [2,0,2]
Output: false

Input: arr = [3,5,5]
Output: false
```
> My Approach
```
1.if is is less than 3 or going downward , it is not a mountain.
2.When we go to a peak, we check the next values are down-ward or not.
```
> My Code
```
class Solution {
public:
    bool validMountainArray(vector<int>& arr) {
        int sz=arr.size();
        
        if(sz<3 || arr[1]<arr[0])
            return false;
        
        int i=0;
        for(; i<sz-1; i++)
        {
            if((arr[i] > arr[i+1]))
            {
                i++;
                break;
            }
            else if(arr[i]==arr[i+1])
                return false;
        }
        
        for(; i<sz; i++)
        {
            if(arr[i-1]<=arr[i])
                return false;
        }
        return true;
    }
};
```
**Task#8**
## Replace Elements with Greatest Element on Right Side

> Sample Input Output
```
Given an array arr, replace every element in that array with the greatest element among the elements to its right, 
and replace the last element with -1.

After doing so, return the array.
Input: arr = [17,18,5,4,6,1]
Output: [18,6,6,6,1,-1]
Explanation: 
- index 0 --> the greatest element to the right of index 0 is index 1 (18).
- index 1 --> the greatest element to the right of index 1 is index 4 (6).
- index 2 --> the greatest element to the right of index 2 is index 4 (6).
- index 3 --> the greatest element to the right of index 3 is index 4 (6).
- index 4 --> the greatest element to the right of index 4 is index 5 (1).
- index 5 --> there are no elements to the right of index 5, so we put -1.

Input: arr = [400]
Output: [-1]
Explanation: There are no elements to the right of index 0.
```

> My Approach
We will use two variable, flag for vector value from last to first.
Mx for max value from flag to last element. Initially it will be -1.
mx will update with maximum value.

> My Code
```
class Solution {
public:
    vector<int> replaceElements(vector<int>& arr) {
        int sz=arr.size(),flag,mx=-1;
       for(int i=sz-1;i>=0;i--)
       {
           flag=arr[i];
           arr[i]=mx;
           mx=max(mx,flag);
       }
        return arr;
    }
};
```

**Task#10**
## Move Zeroes
https://leetcode.com/explore/learn/card/fun-with-arrays/511/in-place-operations/3157/
> Approach

Two Pointer Rule
> Code
```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for (int i=0,j=0; i<nums.size(); i++)
        {
            if(nums[i])
            {
               swap(nums[i],nums[j]);
               j++;
            }
        }
    }
};
```
**Task#11**
## Sort Array by Parity

> Sample Input and Output
```
Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

 

Example 1:

Input: nums = [3,1,2,4]
Output: [2,4,3,1]
Explanation: The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
Example 2:

Input: nums = [0]
Output: [0]
```
> Approach

Two Pointer Rule
> Code
```
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& nums) {
        int i=0;
        if(nums.size()<2)
            return nums;
        
        for(int j=0; j<nums.size();j++)
        {
            if(nums[j] % 2 == 0)
            {
                swap(nums[j],nums[i]);
                i++;
            }
        }
        return nums;
    }
};
```

**Task#12**
## Height Checker

> Sample Input and Output
```
A school is trying to take an annual photo of all the students.The students are asked to stand in a single file line in 
non-decreasing order by height. 
Let this ordering be represented by the integer array expected where expected[i] is the expected height of the ith student in line.

You are given an integer array heights representing the current order that the students are standing in. 
Each heights[i] is the height of the ith student in line (0-indexed).

Return the number of indices where heights[i] != expected[i].

Example 1:

Input: heights = [1,1,4,2,1,3]
Output: 3
Explanation: 
heights:  [1,1,4,2,1,3]
expected: [1,1,1,2,3,4]
Indices 2, 4, and 5 do not match.
```
> Code
```
class Solution {
public:
    int heightChecker(vector<int>& heights) {
        
        if(heights.size()<2)
            return 0;
        
        vector <int> nums(heights);
        sort(nums.begin(),nums.end());
        
        int cnt=0;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]!=heights[i])
                cnt++;
        }
        return cnt;
    }
};
```

