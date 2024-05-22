leetcode 394.Decode String

Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there will not be input like 3a or 2[4].

The test cases are generated so that the length of the output will never exceed 105.

本题是一道中等难度的栈相关模拟题,难点在于处理括号嵌套情况,以下解法使用了两个辅助栈分别记录字符串中出现的字符与数字,相比使用单一辅助栈模拟过程更加清晰,易于理解,时间复杂度为O(n),空间复杂度为O(n).

```java
class Solution {
    public String decodeString(String s) {
        StringBuilder res = new StringBuilder();
        LinkedList<String> stackRes = new LinkedList<>(); // 存字符串
        LinkedList<Integer> stackNum = new LinkedList<>(); // 存数字
        int multi = 0;
        for (Character c : s.toCharArray()) {
            // 当c为'['时,入栈
            if (c == '[') {
                stackNum.addLast(multi);
                stackRes.addLast(res.toString());
                multi = 0;
                res = new StringBuilder();
            }
            // 当c为']'时,出栈
            else if (c == ']') {
                StringBuilder temp = new StringBuilder(); // temp是本次需要倍数重复的字符串
                int cur = stackNum.removeLast();
                for (int i = 0; i < cur; i++) {
                    temp.append(res);
                }
                res = new StringBuilder(stackRes.removeLast()+temp);
            }
            // 记录倍数
            else if (c >= '0' && c <= '9') {
                multi = multi * 10 + Integer.parseInt(c+"");
            }
            // 添加字符
            else {
                res.append(c);
            }
        }
        return res.toString();
    }
}
```