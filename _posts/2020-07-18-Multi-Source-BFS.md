---
layout : post
author : Manash
title : Multi Source BFS.
catrgories : [CSES]
math : true

---

## Codeforces Question : [Christmas Tree](https://codeforces.com/contest/1283/problem/D)

### Tutorial
This particular problem doesn't strike as graph as first. As it has more resemblance to segments. However One of the basic requisites to solve this problem is to observe that we have to assign the nearest positions one by one to all the people. (Greedy).

This is like Prims Algorithm or Dijkstra's Algorithms for finding the MST or Shortest Path Respectively. Hence This kind of concept can be applied when we need to solve a problem in stages. Hence we will store all the distances from a christmas 
trees in a queue. By property of BFS we know that the a current point in the queue has the shortest possible path it could have.

So we keep adding the points and in the result vector and terminate when all people are included.

### Solution

```cpp
	cin >> n;
	int m; cin >> m;
	map<int,int> d;
	queue<int> q;
	vi res;
	for( int i = 0; i < n; ++i) {
		int x;
		cin >> x;
		q.push(x);
		d[x] = 0;
      // THe positions of the tree are at distance == 0;
	}
	int ans = 0;
	while(sz(q)) {
		int u = q.front();
		q.pop();
		int dis = d[u];
		if( dis != 0 ) { // We should not inc the trees.
			ans += dis;
			res.push_back(u);
		}
		for( int i : {1,-1}) {
			if(d.count(u+i)) continue; // Already at shortest distance
			q.push(u+i);
			d[u+i] = dis+1;
		}
		if(sz(res) == m) break;
	}
	cout << ans << '\n';
	for( int x : res ) cout << x << ' ';
```

### Practice Problems :
[Link](https://codeforces.com/contest/1272/problem/E)

[BITMAP](https://www.spoj.com/problems/BITMAP/)
