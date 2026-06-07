# 324. Wiggle Sort II

I got most of the way with this, however

- Had to look up how to interleave a list in place efficiently. The Pythonic way to interleave lists is nifty but not that obvious
- At first I tried to interleave the first half of the list with the second half in order. But you have to interleave the reversed first half with the reversed second half. It's not entirely obvious why that's the case as it seems like on average the distance between interleaved elements would be the same, but it's to do with keeping the middle values maximally apart from each other and it only seems to affect edge cases (both ways work most of the time, and both ways fail if there are two many median values).

``` python
class Solution(object):
    def wiggleSort(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        numslen = len(nums)
        if numslen == 1:
            return
        if numslen == 2:
            if nums[0] < nums[1]:
                return
            else:
                temp = nums[0]
                nums[0] = nums[1]
                nums[1] = temp
                return

        nums.sort()
        mid = (numslen + 1) // 2
        nums[::2], nums[1::2] = nums[mid-1::-1], nums[numslen-1:mid-1:-1]
```