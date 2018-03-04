# Leetcode: Longest Substring with At Most K Distinct Characters     :BLOG:Hard:


---

Longest Substring with At Most K Distinct Characters  

---

Similar Problems:  

-   [Longest Substring with At Most Two Distinct Characters](https://brain.dennyzhang.com/longest-substring-with-at-most-two-distinct-characters)
-   [Tag: #string](https://brain.dennyzhang.com/tag/string)

---

Given an integer array of size n, find all elements that appear more than n/3 times. The algorithm should run in linear time and in O(1) space.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/longest-substring-with-at-most-k-distinct-characters)  

Credits To: [leetcode.com](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: https://brain.dennyzhang.com/longest-substring-with-at-most-k-distinct-characters
    ## Basic Ideas:
    ##
    ## Complexity: Time O(n), Space O(k)
    class Solution:
        def lengthOfLongestSubstringKDistinct(self, s, k):
            """
            :type s: str
            :type k: int
            :rtype: int
            """
            import collections
            import sys
            length = len(s)
            if length <= k: return length
            if k == 0: return 0
            d = collections.defaultdict(lambda: 0)
            index, res = length, -sys.maxsize-1
            for i in range(length):
                ch = s[i]
                if ch in d:
                    d[ch] += 1
                else:
                    if len(d) == k:
                        index = i
                        break
                    else:
                        d[ch] += 1
            res = max(res, self.getCount(d))
    
            j = 0
            for i in range(index, length):
                d[s[i]] += 1
                while len(d) == k+1:
                    ch = s[j]
                    d[ch] -= 1
                    j += 1
                    if d[ch] == 0: del d[ch]
                res = max(res, self.getCount(d))
            return res
    
        def getCount(self, d):
            res = 0
            for ch in d: res += d[ch]
            return res