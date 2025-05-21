# 58.区间和

[题目链接](https://kamacoder.com/problempage.php?pid=1070)

# 题目

题目描述

给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总和。

输入描述

第一行输入为整数数组 Array 的长度 n，接下来 n 行，每行一个整数，表示数组的元素。随后的输入为需要计算总和的区间，直至文件结束。

输出描述

输出每个指定区间内元素的总和。
示例 1
输入

```
5
1
2
3
4
5
1 3
2 4
```

输出

```
6
9
```

# 代码

```javaScript
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 * 前缀和
 * 时间复杂度 O(n)
 * 空间复杂度 O(n)
 * 1. 定义一个数组，用于存放前缀和
 * 2. 监听输入的第一行内容，获取数组的长度
 * 3. 根据输入的长度遍历数组，依次计算前缀和
 * 4. 获取需要计算总和的区间
 * 5. 计算区间内元素的总和
 */
var rangeSum = function() {
  const readline = require('readline');//nodeJS的readline模块
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
  });
  let lines = [];
  rl.on('line', function(line){
    lines.push(line.trim());
  })
  rl.on('close', function(){
    let n = parseInt(lines[0]);
    let sum = [];//存放前缀和
    sum[0] = parseInt(lines[1]);//初始化前缀和 -因为后面计算下标从1开始
    for(let i = 1; i < n; i++){
        sum[i] = sum[i-1] + parseInt(lines[i+1]);
    }
    for(let i = n + 1; i < lines.length; i++){
        let [start, end] = lines[i].split(' ').map(Number);//n个数字之后的每一行都是一个区间 获取区间的起始和结束下标
        if (start === 0) {
            console.log(sum[end]);
        } else {
            console.log(sum[end] - sum[start - 1]);
        }
    }
  })
}

```
