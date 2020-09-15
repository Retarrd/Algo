---
layout : post
author : Manash
title : New Test
catrgories : [CSES]
math : true

---

Check Math :

While $$ a \neq 0$$ and $$ax^2+bx+c = 0$$ has a solution.

Check Code :
```cpp
for( int i = 0; i < n; i++) {
      int x;
      cin >> x;
      vector<int> v; set_bits;
      for( int bit = 0; bit < 32; bit++) {
            if ( (x >> bit ) &1 ) {
                  set_bits.push_back(bit);
      }
      for( int bit : set_bits ) {
            cout << bit << ' ';
      }
      cout << '\n';
}
```
