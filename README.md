# DaysOfCode

## 53. Maximum Subarray - https://leetcode.com/problems/maximum-subarray/

        def maxSubArray(self, nums):
                n=len(nums)
                local_sum=nums[0]
                global_sum=nums[0]

                for i in range(1,n):
                    local_sum=nums[i]+max(local_sum,0)
                    global_sum=max(global_sum,local_sum)
                return global_sum 
