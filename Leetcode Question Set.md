# Leetcode Question Set
----

## [Question 3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

*2021/05/03*

Given a string `s`, find the length of the **longest substring** without repeating characters.

给定字符串s，求不存在重复字符的最长的子字符串

### Note
- 利用两个index来表达一段子字符串；
- 遍历字符串：
    - 每次检查子字符串末尾的字符是否在前文中重复
        - 如果是，则结算两个index之间的距离作为字符串长度，并判断是否是最大字符串；同时更新表达子字符串开始位置的index到字符串中重复出现字符的位置**之后**，并继续循环
    - 递增表达子字符串末尾位置的index
- 直到末尾index达到字符串末尾
- 判断最后一个子字符串的长度是否是最大字符串
- 返回最大字符串


### Code


```python
def lengthOfLongestSubstring(s: str) -> int:
    prob_begin = 0
    prob_end = 0
    max_length = 0
    while prob_end < len(s):
        # calculate
        if s[prob_end] in s[prob_begin:prob_end]:
            #repeat char found
            if max_length < (prob_end - prob_begin):
                max_length = prob_end - prob_begin
            # find the index, put begin prob after the index
            prob_begin += s[prob_begin:prob_end].index(s[prob_end]) + 1
        prob_end += 1
    if max_length < (prob_end - prob_begin):
        max_length = prob_end - prob_begin
    return max_length
```

### Examples
#### 1
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```


```python
lengthOfLongestSubstring("abcabcbb")
```




    3



#### 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```


```python
lengthOfLongestSubstring("bbbbb")
```




    1



#### 3:
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```


```python
lengthOfLongestSubstring("pwwkew")
```




    3



#### 4:
```
Input: s = ""
Output: 0
```


```python
lengthOfLongestSubstring("")
```




    0


