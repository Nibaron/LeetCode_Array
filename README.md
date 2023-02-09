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

Taking advantage of nums[i] <= 10^5(given Constrain)

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

Convert the number to string. Using string.length(), we can find the length.
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
