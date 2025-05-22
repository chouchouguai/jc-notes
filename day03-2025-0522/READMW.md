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
5 //lines[0]
1 //lines[1]
2 //lines[2]
3 //lines[3]
4 //lines[4]
5 //lines[5]
1 3 //求 lines[1] + lines[2] + lines[3]
2 4 //求 lines[2] + lines[3] + lines[4]
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
 * 3. 根据输入的长度遍历数组，依次计算前缀和 放入求和数组对应的位置
 *    -如果是第一个元素，直接赋值(第一位不需要跟前一位求和)
 *    -如果不是第一个元素，当前元素的值= 前一个元素的值(上一次的和)+当前元素的值
 * 4. 获取需要计算总和的区间
 *    -如果是第一个元素，直接输出当前元素的值
 *    -如果不是第一个元素，则区间内元素的总和 = 右边界的值 - （左边界-1）的值
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
    let n = parseInt(lines[0]);//lines[0]是需要输入的数组的长度
    let sum = [];//存放前缀和
    sum[0] = parseInt(lines[1]);//初始化前缀和 -lines[1]是sum[0]数组的第一个元素
    for(let i = 1; i < n; i++){//接下来的n行 每一行是一个数字  从lines[2]开始 要求前缀和
       let num = parseInt(lines[i+1]);//获取当前数字
        sum[i] = sum[i-1] + num//前缀和数组的当前位置的值 = 前一个位置的值 + 当前数字;
    }
    for(let i = n + 1; i < lines.length; i++){
        let [start, end] = lines[i].split(' ').map(Number);//n个数字之后的每一行都是一个区间 获取区间的起始和结束下标
        if (start === 0) {//求和区间从0开始到end结束，也就是lines[1]+...+lines[end],那么前缀数组sum中，sum[end]就是lines[1]+...+lines[end] 直接输出sum[end]
            console.log(sum[end]);
        } else {
            console.log(sum[end] - sum[start - 1]);
        }
    }
  })
}

```
# 44.开发商购买土地
[题目链接](https://kamacoder.com/problempage.php?pid=1044)
# 代码
```javaScript
  /**
   * 1.
   */
var landFunc = function () {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });
    let lines = [];
    rl.on('line', function (line) {
        lines.push(line.trim());
    })
    rl.on('close', function () {
        let [n, m] = lines[0].split(" ").map(Number);

        let col = new Array(n).fill(0);//初始化一个长度为n的数组 每一个元素都是0,每个元素代表一行中的内容,因为后续这个col数组是用来存放每一行中m列元素的和,有n行 col中就有n个值
        let row = new Array(m).fill(0);//初始化一个长度为m的数组 每一个元素都是0,每个元素代表一列中的内容
        let arr = new Array(n);
        let sum = 0//数组总和
        //接受每一行的输入,转为数组,存入arr数组中,但是自己输入的时候要记得输入的列数不要超过m
        for (let i = 0; i < n; i++) {
            arr[i] = lines[i + 1].split(' ').map(Number);//最终arr是一个二维数组
        }
        // console.log(arr);
        //每一行的和
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                col[i] += arr[i][j]// 每行权重之和
                sum += arr[i][j]//所有权重之和
            }
        }
        console.log('---col', col);
        console.log('---sum', sum);
        //每一列的和
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                row[j] += arr[i][j]
            }
        }
        let sum1 = 0, sum2 = 0;//横/纵向切割之和
        for (let i = 0; i < n; i++) {
            sum1 += col[i]；//横向切割权重之和
            //假设衡切上下部分的权重一样 均为sum1  sum-2*sum1 就是切割后两部分的权重之差
            min = min < Math.abs(sum - 2 * sum1) ? min : Math.abs(sum - 2 * sum1)
        }
        //同理分析纵向切割
        for (let j = 0; j < m; j++) {
            sum2 += row[j]
            min = min < Math.abs(sum - 2 * sum2) ? min : Math.abs(sum - 2 * sum2)
        }
        console.log(min);

    })
}
  landFunc();
```
# 203 移除链表元素
[题目链接](https://leetcode.cn/problems/remove-linked-list-elements/description/)
# 代码
```javaScript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}
 * 虚拟头节点
 * 时间复杂度 O(n)
 * 空间复杂度 O(1)    
 * 1. 定义一个虚拟头节点，用于存放链表的头节点
 * 2. 定义一个指针，用于遍历链表
 * 3. 遍历链表，如果当前节点的值等于val，则将当前节点的前一个节点的next指向当前节点的next
 * 4. 返回虚拟头节点的next
 */
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
var removeElements = function(head, val) {
  const ret = new ListNode(0, head);
    let cur = ret;
    while(cur.next) {
        if(cur.next.val === val) {
            cur.next =  cur.next.next;
            continue;
        }
        cur = cur.next;
    }
    return ret.next;
}