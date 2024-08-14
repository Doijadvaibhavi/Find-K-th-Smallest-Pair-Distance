# Find-K-th-Smallest-Pair-Distance
The distance of a pair of integers a and b is defined as the absolute difference between a and b.

Given an integer array nums and an integer k, return the kth smallest distance among all the pairs nums[i] and nums[j] where 0 <= i < j < nums.length.

 
Example 1:

Input: nums = [1,3,1], k = 1

Output: 0

Explanation: Here are all the pairs:

(1,3) -> 2

(1,1) -> 0

(3,1) -> 2

Then the 1st smallest distance pair is (1,1), and its distance is 0.

Example 2:

Input: nums = [1,1,1], k = 2

Output: 0

Example 3:

Input: nums = [1,6,1], k = 3

Output: 5
 

Constraints:

n == nums.length

2 <= n <= 104

0 <= nums[i] <= 106

1 <= k <= n * (n - 1) / 2

# SOLUTION 

* Binary Search: We use binary search to find the smallest distance such that there are at least k pairs with that distance or smaller.

* Two-Pointer Technique: Within the binary search, we use the two-pointer technique to count how many pairs have a distance less than or equal to the middle value of the current binary search range.

* Approach
  
Sort the Array: Sorting simplifies the calculation of distances between elements.

* Binary Search on Distance:
  
Set the initial range of possible distances (low = 0 to high = max distance in the array).

Find the middle distance (mid) and count how many pairs have a distance less than or equal to mid.

* Count Pairs:
  
Use the two-pointer technique to count the number of pairs with a distance less than or equal to mid.

If the count is less than k, it means we need to search for a larger distance, so move the lower bound (low) up.

If the count is greater than or equal to k, move the upper bound (high) down.

Terminate: The binary search converges when low == high, giving us the k-th smallest distance.

# JAVA CODE

class Solution {

    public int smallestDistancePair(int[] nums, int k) {
    
        Arrays.sort(nums);
        
        int n = nums.length;
        
        int low = 0, high = nums[n - 1] - nums[0];

        while (low < high) {
        
            int mid = low + (high - low) / 2;
            
            if (countPairs(nums, mid) < k) low = mid + 1;
            
            else high = mid;
        }

        return low;
    }

    private int countPairs(int[] nums, int maxDistance) {
    
        int count = 0, j = 0;
        
        for (int i = 0; i < nums.length; ++i) {
        
            while (j < nums.length && nums[j] - nums[i] <= maxDistance) ++j;
            
            count += j - i - 1;
        }
        
        return count;
    }
}
