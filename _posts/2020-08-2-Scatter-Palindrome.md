---
layout : post
author : Manash
title : Scatter Palindrome
catrgories : [CSES]
math : true

---

## Problem Description

A palindrome is a string which reads the same forward and backwards, for example, $tacocat$ and          $mom$. A string is a  scatter-palindrome if its letters can be rearranged to form a palindrome. Given a string, determine how many of its  substrings are scatter-palindrome. A substring is a contiguous range of characters within the string.

For example, given a string $aabb$ the scatter-palindromes are $a,aa,aab,aabb,a,abb,b,,bb,b$.

there are 9 substrings that are scatter-palindromes.

Write a program that takes input in the below given format and prints output in the below given format.

​       Constraints 

-  $1≤size of string≤1000$

 The string contains lower-case alphabets. 

## Tutorial

This is also a variant of the standard DP problem of counting palindromes. The required condition of a string to be a palindrome or an anagram of a palindrome is that it should contain at most 1 odd occurrence of any character.

Also a string of length 1 is always a palindrome.

So with a naive approach we can check for every possible substring and check if it's a palindrome using the above condtions. We can speed this up using dynamic programming, as the recurrence is also trivial.

$$
cnt[i][j][ch] = (s[i] == ch) + cnt[i+1][j][ch], \forall \; ch \in [a,z]
$$

Where $cnt[i][j][ch]$ represents the number of occurrences of character $ch$ in the range $i$ to $j$. 

Rest what is left to check the validity of the string, which can be done checking all the characters and counting the number of odd characters.

## Solution

```cpp

int n;
const int nax = 1001;
bool dp[nax][nax];
int cnt[nax][nax][26];
void test() {
      string s; cin >> s; n = sz(s);
      for( int i = 0; i < n; i++) {
            dp[i][i] = 1;
            cnt[i][i][s[i]-'a'] = 1;
      }
      for( int len = 2; len <= n; len++) {
            for( int i = 0; i < n; i++) {
                  int j = i + len - 1;
                  if ( j >= n) break;
                  for( int ch = 0; ch < 26; ch++) {
                        cnt[i][j][ch] += cnt[i+1][j][ch];
                  }
                  cnt[i][j][s[i]-'a']++;
                  int odd = 0;
                  for( int ch = 0; ch < 26; ch++) {
                        if(cnt[i][j][ch]&1) {
                              if(++odd == 2 ) {
                                    dp[i][j] = 0;
                                    break;
                              }
                        }
                  }
                  if(odd < 2 ) dp[i][j] = 1;
            }
      }
      int ans = 0;
      for( int i = 0; i < n; i++) {
            for( int j = 0; j <= i; j++) {
                  ans += dp[j][i];
            }
      }
      cout << ans;
}

```

