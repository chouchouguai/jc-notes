# jc-notes
代码随想刷题
* 时间复杂度:衡量算法运行时间随输入规模增长而变化的数学表示，用于分析算法的效率。它不计算具体时间（如秒或毫秒），而是关注​​操作次数的增长趋势​​。
复杂度​​	    ​​数学表示​​	​       ​    示例算法​​
常数时间	    O(1)	            数组随机访问（arr[i]）
对数时间	    O(log n)	        二分查找
线性时间	    O(n)	            遍历数组
线性对数时间	 O(n log n)	         快速排序、归并排序
平方时间	    O(n²)	            冒泡排序、嵌套循环
指数时间	    O(2ⁿ)	            穷举搜索（如斐波那契递归）
阶乘时间	    O(n!)	            旅行商问题（暴力解法）

* 空间复杂度:衡量算法运行所需内存空间随输入规模增长而变化的数学表示，用于分析算法的内存使用效率。它不计算具体内存大小（如字节或千字节），而是关注​​数据结构的大小​​。
​​复杂度​​	​       ​示例场景​​	​       ​典型算法​​
​​O(1)​​	    固定大小的临时变量	交换两个变量（a, b = b, a）
​​O(n)​​	    额外数组或哈希表	归并排序的临时数组
​​O(log n)​​	递归调用栈的深度	二分查找的递归实现
​​O(n²)​​	    二维数组或嵌套结构	动态规划中的二维 DP 表
