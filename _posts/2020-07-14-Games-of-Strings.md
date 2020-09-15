---
layout : post
author : Manash
title : Games on String
catrgories : [CSES]
math : true
---



### [Problem Statement](https://codeforces.com/problemset/problem/930/B)



#### Tutorial

As with all questions go. To move forward in this questions. Let's determine the parameters we have to deal with. We propose the following.

* The first character $c_1$
* The second character $c_2$
* The distance between them in the original string $d$ 

So for example if decide to fix the first character $c_1$ and the distance $d$, we will be left with some choices of $c_2$, Some of them maybe unique, and other may not. It's easy to see that Vasya will only win when $c_2$ is unique.

So for a fixed $c_1$ and $d$, the probability of winning is 

$$P = \dfrac{|\{c_2 : |c2| = 1\}|}{|\{c_2\}|}$$ 

Let $p=\lvert\{c_2:\lvert c2 \rvert=1\}\rvert$. 

Here we can see that to maximise the probability of winning, the optimal way is to choose the $max(p)$ overall all the values of $d$. This step gives us a fixed value of d for all $c_1$. 

So all that is left is to iterate over all values of $c_1$. Where the probability of choosing a $c_1$ is $\dfrac{cnt(c_1)}{n}$. And add all the values. 

$P = \sum \dfrac{cnt(c_1)}{n} \times \dfrac{p}{cnt(c1)} = \sum \dfrac{p}{n}$ 

( Notice how $cnt(c_1)=\lvert\{c_2\}\rvert$ ) 

### Implementation

```cpp
int f[26][5001][26];
int main () { _read();

      string s; cin >> s;
      int n = sz(s);
      vector<char> vec(A(s));
      sort(A(vec)); vec.erase(unique(A(vec)),vec.end());
      for( int i = 0; i < n; i++) {
            for (int d = 1; d < n; d++) {
                  int j = (i+d) % n;
                  f[s[i]-'a'][d][s[j]-'a']++;
            }
      }
      double ans = 0;
      for ( char c : vec ) {
            int mx = 0;
            for (int d = 1; d < n; ++d) {
                  int h = 0;
                  for( int c2 = 0; c2 < 26; c2++) {
                        h += (f[c-'a'][d][c2] == 1);
                  }
                  mx = max(mx,h);
            }
            ans += 1.0*mx/n;
      }
      cout << fixed << setprecision(12) << ans << '\n';
      return 0;
};
```



