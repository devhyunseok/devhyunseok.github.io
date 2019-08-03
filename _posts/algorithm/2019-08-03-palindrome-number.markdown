---
layout: post
title:  "Palindrome Number"
author: Hyunseok
categories: algorithm
comments: false
---

<h1>Palindrome Number</h1>
<h4>난이도 : Easy</h4>
---
<p>
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.</p>
<p>
정수가 팔레드롬인지 결정. 정수는 앞,뒤로 동일하게 읽을 떄 팔레드롬이다.
</p>
---
<h4>Example 1</h4>
<pre>
<code>Input: 121
Output: true
Example 2:
</code>
</pre>

<h4>Example 2</h4>
<pre>
<code>Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
</code>
</pre>

<h4>Example 3</h4>
<pre>
<code>Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
</code>
</pre>

---

<h2>Solution</h2>
<h4>언어: Javascript</h4>
<h4>출처 : <a href="https://leetcode.com/problems/palindrome-number/">Leetcode</a></h4>
<pre>
<code>/**
 * @param {number} x
 * @return {boolean}
 */
const isPalindrome = function(x) {
    if (x === 0) return true; // 0일땐 항상 true
    if (x < 0 || x % 10 === 0) return false; // 음수거나 10으로 나눠서 나머지가 없을 경우 항상 false
    
    const stringNum = x.toString();
    const reverse = stringNum.split('').reverse().join('');

    return toStringInput === reverse;
};
</code>
</pre>