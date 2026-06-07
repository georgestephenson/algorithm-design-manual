# 739. Daily Temperatures

https://leetcode.com/problems/daily-temperatures/

## Canonical Solution

``` python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        result = [0] * len(temperatures)
        stack = []  # indices of unresolved days (temperatures are decreasing)

        for i, temp in enumerate(temperatures):
            # While current temp is warmer than the temp at stack's top index...
            while stack and temperatures[stack[-1]] < temp:
                prev_idx = stack.pop()
                result[prev_idx] = i - prev_idx  # days to wait = distance
            stack.append(i)

        # Anything left in stack never found a warmer day → stays 0
        return result
```

The initial "result" assumes

## Initial attempts

I initially played around with dictionaries before realising this chapter is probably pointing towards a recursive solution:

``` python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        if len(temperatures) == 1:
            return [0]
        else:
            this = temperatures[0]
            result = 0
            for idx, i in enumerate(temperatures[1:]):
                if (i>this):
                    result = idx + 1
                    break
            return [result] + self.dailyTemperatures(temperatures[1:])
```

That works but performance is terrible (memory limit exceeded on LeetCode).

Then I remembered that tail-recursion can always be written iteratively which will use less memory. And that managing this with list pointers is always faster than creating many lists. This is all obvious...

``` python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        i = 0
        imax = len(temperatures)-1
        result = []
        while i < imax:
            for j in range(i+1,imax+1):
                if (temperatures[j] > temperatures[i]):
                    result.append(j-i)
                    break
            else:
                result.append(0)
            i += 1
        result.append(0)
        return result
```

But it still fails with "time limit exceeded".

I went back to the dictionary idea:

``` python
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        imax = len(temperatures)-1
        i = imax-1
        d = dict()
        result = [0]
        while i >= 0:
            thisTemp = temperatures[i]
            thisMax = imax+1
            default = 0
            if thisTemp in d:
                (lastResult, lastIdx) = d[thisTemp]
                if lastResult > 0:
                    default = lastResult + (lastIdx - i)
                    thisMax = lastIdx
            for j in range(i+1,thisMax):
                if (temperatures[j] > thisTemp):
                    thisResult = j-i
                    break
            else:
                thisResult = default
            result.append(thisResult)
            d[thisTemp] = (thisResult, i)
            i -= 1
        return list(reversed(result))
```

Still too slow. I knew this was pointing towards traversing the list while having a data structure to remember previous temperatures, but rather than remembering previous results, it's enough to remember unresolved temperatures in a stack and resolve them later.