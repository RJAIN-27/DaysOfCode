# DaysOfCode

#### 53. Maximum Subarray - https://leetcode.com/problems/maximum-subarray/

        def maxSubArray(self, nums):
                n=len(nums)
                local_sum=nums[0]
                global_sum=nums[0]

                for i in range(1,n):
                    local_sum=nums[i]+max(local_sum,0)
                    global_sum=max(global_sum,local_sum)
                return global_sum 

#### 918. Maximum Sum Circular Subarray - https://leetcode.com/problems/maximum-sum-circular-subarray/

        def maxSubarraySumCircular(self, A):
                sub_max = A[0]    
                max_sum = A[0]
                sub_min = A[0]
                min_sum = A[0]
                total_sum = A[0]

                for num in A[1:]:
                    total_sum += num
                    sub_max = max(num, sub_max + num)
                    max_sum = max(max_sum, sub_max)

                    sub_min = min(num, sub_min + num)
                    min_sum = min(min_sum, sub_min)

                if total_sum - min_sum > max_sum and total_sum - min_sum!=0:
                    return total_sum - min_sum
                else:
                    return max_sum
