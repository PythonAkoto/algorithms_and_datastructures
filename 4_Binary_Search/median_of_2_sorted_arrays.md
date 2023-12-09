# 4. Median of Two Sorted Arrays
## Company: Meta

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

 

Example 1:

Input: `nums1 = [1,3], nums2 = [2]`
Output: `2.00000`
Explanation: merged array = `[1,2,3]` and median is `2`.
Example 2:

Input: `nums1 = [1,2], nums2 = [3,4]`
Output: `2.50000`
Explanation: merged array = `[1,2,3,4]` and median is `(2 + 3) / 2 = 2.5`.

# Python 
```
# Time complexity: O(log(min(n, m)))
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        # Make sure nums1 is the smaller array
        A, B = nums1, nums2
        total = len(nums1) + len(nums2)
        half = total // 2

        if len(B) < len(A):
            A, B = B, A

        # Initialize pointers for binary search
        l, r = 0, len(A) - 1

        # Perform binary search
        while True:
            i = (l + r) // 2  # Pointer for array A
            j = half - i - 2  # Pointer for array B

            # Get values for partitioning
            Aleft = A[i] if i >= 0 else float("-infinity")
            Aright = A[i + 1] if (i + 1) < len(A) else float("infinity")
            Bleft = B[j] if j >= 0 else float("-infinity")
            Bright = B[j + 1] if (j + 1) < len(B) else float("infinity")

            # Check if the partition is correct
            if Aleft <= Bright and Bleft <= Aright:
                # If the total number of elements is odd, return the smaller of Aright and Bright
                if total % 2:
                    return min(Aright, Bright)
                # If the total number of elements is even, return the average of the larger of Aleft and Bleft and the smaller of Aright and Bright
                return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
            elif Aleft > Bright:
                # Adjust the pointers for binary search
                r = i - 1
            else:
                # Adjust the pointers for binary search
                l = i + 1
```

# JavaScript
```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * Time O(log(N * M)) | Space O(N)
 * @return {number}
 */
var findMedianSortedArrays = function (nums1, nums2) {
    const canSwap = nums2.length < nums1.length;
    if (canSwap) [nums1, nums2] = [nums2, nums1];

    let [left, right] = [0, nums1.length - 1];
    const totalLength = nums1.length + nums2.length;
    const mid = totalLength >> 1;
    const isEven = totalLength % 2 === 0;

    while (true) {
        const mid1 = left + right;
        const mid2 = mid - mid1 - 2;
        const { aLeft, aRight, bLeft, bRight } = getPointers(
            nums1,
            mid1,
            nums2,
            mid2
        );

        const isTarget = aLeft <= bRight && bLeft <= aRight;
        if (isTarget)
            return isEven
                ? (Math.max(aLeft, bLeft) + Math.min(aRight, bRight)) / 2
                : Math.min(aRight, bRight);

        const isTargetGreater = aLeft <= bRight;
        if (isTargetGreater) left = mid1 + 1;

        const isTargetLess = bRight < aLeft;
        if (isTargetLess) right = mid1 - 1;
    }
};

const getPointers = (nums1, mid1, nums2, mid2) => {
    const getLeft = (nums, index) => (0 <= index ? nums[index] : -Infinity);

    const [aLeft, bLeft] = [getLeft(nums1, mid1), getLeft(nums2, mid2)];

    const getRight = (nums, index) =>
        index + 1 < nums.length ? nums[index + 1] : Infinity;

    const [aRight, bRight] = [getRight(nums1, mid1), getRight(nums2, mid2)];

    return { aLeft, aRight, bLeft, bRight };
};
```