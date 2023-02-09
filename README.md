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
