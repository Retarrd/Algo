---
layout : post
author : Manash
title : Dima and Hares
catrgories : [CSES]
math : true

---
<h2> Problem Statement </h2>
There are hares numbered from 1 to n ready to be fed.

Inna noticed that each hare radiates joy when she feeds it. And the joy of the specific hare depends on whether Inna fed its adjacent hares before feeding it. Inna knows how much joy a hare radiates if it eats when either both of his adjacent hares are hungry, or one of the adjacent hares is full (that is, has been fed), or both of the adjacent hares are full. Please note that hares number 1 and n don't have a left and a right-adjacent hare correspondingly, so they can never have two full adjacent hares.

Help Inna maximize the total joy the hares radiate.
The 3 arrays represent the respective values when $\{0,1,2\}$ of the adjacents hares are fed.

<h3> Sample Input </h3>

```
4
1 2 3 4
4 3 2 1
0 1 1 0
```
<h3> Sample Output </h3>

```
7
```

<h2> Tutorial </h2>

Here We will use Dynamic Programming to Solve this problem.

Let's say we are currently feeding the $ith$ hare, starting from the suffix. There Are Two Possiblites for $({i-1})th$ hare. It's either <em>fed</em>, or it's <em>not fed</em>.

Hence We can determine the states of the DP. it will have two states <br>
1) ```bool prev ```  : Denoting where the last hare is fed or unfed. <br>
2) ```int i ``` : Denoting the index which we are working on.

So from this the transitions are as follows,

$dp[i][0] = max\, (\,dp[i+1][1] + a[i],\;dp[i+1][0]+b[i]\,)$<br>
$dp[i][1] = max\, (\,dp[i+1][1] + b[i],\;dp[i+1][0]+c[i]\,)$

The final answer will lie in $dp[0][0]$ and the base cases are for $dp[n-1][0] = a_n \text{ and }dp[n-1][1] = b_n$

## Solution

```cpp
void test() {
	
	int n;
	cin >> n;
	int a[n],b[n],c[n];
	for( int i = 0; i < n; i++) cin >> a[i];
	for( int i = 0; i < n; i++) cin >> b[i];
	for( int i = 0; i < n; i++) cin >> c[i];
 
	int dp[n+1][2];
	mem(dp,0);
	dp[n-1][0] = a[n-1];
	dp[n-1][1] = b[n-1];
	for( int i = n-2; i >= 0; i--) {
		dp[i][0] = max(dp[i+1][0]+b[i],dp[i+1][1]+a[i]);
		dp[i][1] = max(dp[i+1][0]+c[i],dp[i+1][1]+b[i]);
	}
	cout << dp[0][0];
}
```