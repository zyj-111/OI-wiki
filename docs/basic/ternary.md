给定函数 $f(x)$ ，该函数在区间 $[l, r]$ 是单峰函数。求其在区间上的最大值。

## 算法

先随便找两个点 $m_1$ , $m_2$ ($l < m_1 < m_2 < r$)，这两个点把区间分成了三份。然后计算 $f(m_1)$ 和 $f(m_2)$ ：
-   $f(m_1) < f(m_2)$

    最大值不可能在 $m_1$ 左边。范围缩小至 $[m_1, r]$ 。
-   $f(m_1) > f(m_2)$

    最大值不可能在 $m_2$ 右边。范围缩小至 $[m_1, r]$ 。

-   $f(m_1) = f(m_2)$

    范围缩小至 $[m_1, m_2]$ 。

因此我们就把区间从 $[l, r]$ 缩小至了 $[l^\prime, r^\prime]$ ，一直这样迭代下去，就可以在规定精度的条件下得到函数的最大值。

至于起始点怎么选择，最常见的选择办法就是两个三等分点：

$$m_1 = l + \frac{(r - l)}{3}$$

$$m_2 = r - \frac{(r - l)}{3}$$ 

### 复杂度

$$T(n) = T({2n}/{3}) + 1 = O(\log n)$$

该公式应用了 [Master's Theorem](https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms))，从而我们得到了所期望的时间复杂度。

### 整数区间

如果 $f(x)$ 的自变量只能是整数，连续区间 $[l, r]$ 就变成了离散区间，我们就需要修改一下算法的停止条件即 $(r - l) < 3$ 。


??? note "参考代码"
	```cpp
	double ternary_search(double l, double r) {
		double eps = 1e-9;//精度
		while (r - l > eps) {
			double m1 = l + (r - l) / 3;
			double m2 = r - (r - l) / 3;
			double f1 = f(m1);
			double f2 = f(m2);
			if (f1 < f2)
				l = m1;
			else
				r = m2;
		}
		return f(l);
	}
	```

## 练习题

- [Codechef - Race time](https://www.codechef.com/problems/AMCS03)
- [Hackerearth - Rescuer](https://www.hackerearth.com/september-circuits/algorithm/rescuer-1/)
- [Spoj - Building Construction](http://www.spoj.com/problems/KOPC12A/)
- [Codeforces - Weakness and Poorness](http://codeforces.com/problemset/problem/578/C)
* [LOJ - Closest Distance](http://lightoj.com/volume_showproblem.php?problem=1146)
* [GYM - Dome of Circus (D)](http://codeforces.com/gym/101309)
* [UVA - Galactic Taxes](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=4898)
* [GYM - Chasing the Cheetahs (A)](http://codeforces.com/gym/100829)
* [UVA - 12197 - Trick or Treat](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=3349)
* [SPOJ - Building Construction](http://www.spoj.com/problems/KOPC12A/)
* [Codeforces - Devu and his Brother](https://codeforces.com/problemset/problem/439/D)
* [Codechef - Is This JEE ](https://www.codechef.com/problems/ICM2003)
* [Codeforces - Restorer Distance](https://codeforces.com/contest/1355/problem/E)


**本页面主要译自博文[Тернарный поиск](http://e-maxx.ru/algo/ternary_search)与其英文翻译版[Ternary Search](https://cp-algorithms.com/num_methods/ternary_search.html)。其中俄文版版权协议为 Public Domain + Leave a Link；英文版版权协议为 CC-BY-SA 4.0。** 
