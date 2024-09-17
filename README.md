Intuition

The task is to find two numbers in an array that sum up a given target. 
The key insight is that for each number in the array, there is a complementary number that, when added to it, equals the target. 
If we can efficiently check if this complementary number has already been encountered, we can solve the problem in one pass through the array. 

Approach

In an unordered_map (hash map), we store each number we encounter in the array and its index.

As we iterate through the array, we calculate the complement for each number (i.e., target - current number).

If the complement already exists in the map, we have previously encountered the number that, together with the current number, sums to the target.

We then return the indices of the two numbers (the index of the complement from the map and the current index).

If the complement is not found, we store the current number and index in the map for future lookup.
Complexity

    Time complexity:
    O(n) where n is the number of elements in the input array nums. This is because we are iterating through the array once, and hash map operations (insertion and lookup) have an average time complexity of O(1).

    Space complexity:
    O(n) due to the space needed to store up to n elements in the hash map.

Code

#include <vector>
#include <unordered_map>

class Solution {
public:
    // This function finds two indices in the nums vector such that their corresponding values add up to the target.
    // If found, it returns the indices of these two numbers as a vector of size 2.
    std::vector<int> twoSum(std::vector<int>& nums, int target) 
{
        // Create an unordered_map to store the number and its index.
        // The key is the number, and the value is the index of that number in the nums array.
        std::unordered_map<int, int> num_map {}; // num_map[number] = index

        // Iterate over the nums array to find the two numbers that sum up to the target.
        for (int i = 0; i < static_cast<int>(nums.size()); ++i)
        {
            // Calculate the complement of the current element.
            // The complement is the number that needs to be added to nums[i] to get the target.
            int complement = target - nums[i];

            // Check if the complement is already in the map.
            // If it is, that means we've found the two numbers whose sum equals the target.
            if (num_map.find(complement) != num_map.end())
            {
                // If the complement is found, return the indices of the complement and the current number.
                // num_map[complement] gives the index of the complement, and 'i' is the index of the current number.
                return {num_map[complement], i};
            }

            // If the complement is not found, store the current number with its index in the map.
            // This way, we can check for this number as a complement in future iterations.
            num_map[nums[i]] = i;
        }

        // Return an empty vector if no solution is found (though this case should not occur per problem constraints).
        return {};
    }
};
