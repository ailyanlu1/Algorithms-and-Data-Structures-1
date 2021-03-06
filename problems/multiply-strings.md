# Multiply Strings - from [LeetCode](https://leetcode.com)
[View this problem on LeetCode](https://leetcode.com/problems/multiply-strings/)

## Description
Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.

## Thinking & Notes
* for loop: the key idea is regular multiplication concept. start from the back of two strings, multiply two digit, put into last two cells.
  - `num1[i] * num2[j]` will be placed at indices `[i + j`, `i + j + 1]`
* Break down of solution I: same idea, but easier to understand

## Solution - for loop
```java
class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length(), len2 = num2.length();
        int[] arr = new int[len1 + len2];
        
        for (int i = len1 - 1; i >= 0; i--){
            for (int j = len2 - 1; j >= 0; j--){
                int multi = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                int p1 = i + j, p2 = i + j +1;
                int sum = multi + arr[p2];
                
                arr[p1] += sum / 10;
                arr[p2] = sum % 10;
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (int n : arr) if (!(sb.length() == 0 && n == 0)) sb.append(n+"");
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```
#### Complexity
* Time Complexity: O(m*n)
* Space Complexity: O(m+n)

## Solution - Break down of solution I
```java
class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length(), len2 = num2.length();
        int[] product = new int[len1 + len2];
        
        // get product of every pair
        for (int i = len1 - 1; i >= 0; i--){
            for (int j = len2 - 1; j >= 0; j--){
                int n1 = num1.charAt(i) - '0';
                int n2 = num2.charAt(j) - '0';
                product[i+j+1] += n1 * n2;
            }
        }
        
        // add carry
        int carry = 0;
        for (int i = product.length - 1; i >= 0; i--){
            int temp = (product[i] + carry) % 10;
            carry = (product[i] + carry) / 10;
            product[i] = temp;
        }
        
        StringBuilder sb = new StringBuilder();
        for (int n : product) if (!(sb.length() == 0 && n == 0)) sb.append(n);
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```
#### Complexity
* Time Complexity: O(m*n)
* Space Complexity: O(m+n)
