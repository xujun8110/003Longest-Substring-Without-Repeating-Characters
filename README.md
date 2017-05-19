# 003Longest-Substring-Without-Repeating-Characters
Given "pwwkew", the answer is "wke", with the length of 3. 
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

来到了第三题，第一次看题目以为求不重复最长字符子序列长度，还以为用TreeSet直接出来这么弱的题目...
求最长子串，直接暴力解法...算了不解释
一边遍历，从左向右扫描，start表示了出现重复后的下一个字母开始子字符串，
很重要的一点是在新的子字符串中检测，不能包含之前的字符，（开始abba用例通不过），通过start取的新值不能比之前的小体现，即取一个max即可。
维护一个最长长度即可。

上代码吧
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int start = 0, ans = 0;
        
        for(int i = 0; i < s.length(); i++) {
            if(map.containsKey(s.charAt(i))) {
            //关键的一步，之前没有想好如何实现只在新的子字符串中检测，没通过abba用例
                start = Math.max(start, map.get(s.charAt(i)) + 1);
            }
            ans = Math.max(ans, i - start + 1);
            map.put(s.charAt(i), i);
        }
        return ans;
    }
}
