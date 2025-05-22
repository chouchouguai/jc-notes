# 977. 有序数组的平方

> 难度：简单

## 题目

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

**示例 1：**

```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

**示例 2：**

```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

### 代码

#### 方法一：暴力法

```JavaScript
/**
 * @param {number[]} nums
 * @return {number[]}
 * 遍历数组的每个元素，将每个元素平方后存入新数组
 * 对新数组进行排序
 * 返回新数组
 */
var sortedSquares = function(nums) {
    return nums.map(num => num * num).sort((a, b) => a - b);
};

```

#### 方法二：双指针法

```JavaScript
/**
 * @param {number[]} nums
 * @return {number[]}
 * 因为数组有序 ，所以平方后最大的元素一定在数组的两端
 * 1. 定义两个指针，一个指向数组的开头，一个指向数组的末尾
 * 2. 定义一个新数组，用于存放平方后的元素
 * 3. 比较两个指针指向的元素的平方，将较大的平方存入新数组的末尾，并将对应的指针向中间移动
 * 4. 重复步骤3，直到两个指针相遇
 * 5. 返回新数组
 */
var sortedSquares = function(nums) {
    let left=0,right=nums.length-1,idx=nums.length-1,result=[];
    while(left<=right){
        let leftSqu = Math.pow(nums[left],2);
        let rightSqu = Math.pow(nums[right],2);
        if(leftSqu > rightSqu){
            result[idx--] = leftSqu;
            left++;
        }else{
            result[idx--] = rightSqu;
            right--;
        }
    }
    return result;
};
```

# 209.长度最小的子数组

[题目链接](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)

> 难度：中等

## 代码

## 方法：滑动窗口

```JavaScript
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 * 滑动窗口
 * 时间复杂度 O(n)
 * 空间复杂度 O(1)
 * 1. 定义两个指针，一个指向数组的开头，一个指向数组的末尾(注意这个末尾是指向窗口的末尾，不是指向nums数组的末尾)
 * 2. 定义一个变量，用于存放窗口内的元素之和sum
 * 3. 定义一个变量，用于存放最小窗口的长度resultLength(默认为无穷大，表示没有符合条件的窗口)
 * 4. 遍历(a)数组，将元素加入窗口，并更新窗口内的元素之和
 * 5. 如果窗口内的元素之和大于等于target，（遍历(b)执行）
 *    - 5.1 更新窗口的长度resultLength
 *    - 5.2 将窗口的左指针向右移动，直到窗口内的元素之和小于target(退出遍历b)
 *       -这一步的目的是在右指针不变的情况下，找到符合条件最短的窗口，使得窗口内的元素之和大于等于target
 *     - 5.3 更新窗口的长度resultLength
 * 6. 如果窗口内的元素之和小于target，则将窗口的右指针向右移动，直到窗口内的元素之和大于等于target(进入遍历b)
 * 7. 返回窗口的长度
 */
var minSubArrayLen = function(target, nums) {
    let left=0,right=0,sum=0,len=nums.length,resultLength=Infinity;
    while(right<len){
        sum+=nums[right];
        while(sum>=target){
            resultLength = Math.min(resultLength,right-left+1);
            sum-=nums[left];
            left++;
        }
        right++;
    }
    return resultLength===Infinity?0:resultLength;
};
```

# 59.螺旋矩阵 II

[题目链接](https://leetcode.cn/problems/spiral-matrix-ii/description/)

> 难度：中等

## 代码

## 方法：模拟

```JavaScript
/**
 * @param {number} n
 * @return {number[][]}
 * 模拟
 * 时间复杂度 O(n^2)
 * 空间复杂度 O(n^2)
 * 1. 定义一个二维数组，用于存放螺旋矩阵
 * 2. 定义四个变量，分别表示螺旋矩阵的上下左右边界，定义一个变量，用于存放螺旋矩阵的元素
 * 3. 遍历螺旋矩阵的每一层，从左到右，从上到下，从右到左，从下到上
 * 4. 返回螺旋矩阵
 */
var generateMatrix = function(n) {
    let matrix = new Array(n).fill(0).map(() => new Array(n).fill(0));//创建一个n*n的二维数组
    let left=0,right=n-1,top=0,bottom=n-1,num=1;
    while(left<=right && top<=bottom){
        for(let i=left;i<=right;i++){//从左到右，填充上边界
            matrix[top][i] = num++;
        }
        for(let i=top+1;i<=bottom;i++){//从上到下，填充右边界
            matrix[i][right] = num++;
        }

        if(left<right && top<bottom){//当不是单行或单列时，才需要填充下边界和左边界
            for(let i=right-1;i>=left;i--){//从右到左，填充下边界
                matrix[bottom][i] = num++;
            }
            for(let i=bottom-1;i>top;i--){//从下到上，填充左边界
                matrix[i][left] = num++;
            }
        }
        left++;
        right--;
        top++;
        bottom--;
        }
        return matrix;
}
```

## 随想录代码

```JavaScript
/**
 * @param {number} n
 * @return {number[][]}
 * 模拟
 * 时间复杂度 O(n^2)
 * 空间复杂度 O(n^2)
 * 1. 定义一个二维数组，用于存放螺旋矩阵
 * 2. 定义四个变量，分别表示螺旋矩阵的上下左右边界，定义一个变量，用于存放螺旋矩阵的元素
 * 3. 遍历螺旋矩阵的每一层，从左到右，从上到下，从右到左，从下到上
 * 4. 返回螺旋矩阵
 */
var generateMatrix2 = function(n) {
    let res = new Array(n).fill(0).map(() => new Array(n).fill(0));//创建一个n*n的二维数组
    let startX = 0, startY = 0;//定义每循环一个圈的起始位置(x,y)坐标
    let loop = Math.floor(n / 2);//定义循环的圈数
    let mid = Math.floor(n / 2);//定义中间位置的坐标
    let count = 1;//定义填充数字增量
    let offset = 1;//定义每一圈循环，每条边遍历的长度
    while(loop--) {
        let row = startX, col = startY;
        for(; col <  n - offset; col++) {//从左到右，填充上边界
            res[row][col] = count++;
        }
        for(; row <  n - offset; row++) {//从上到下，填充右边界
            res[row][col] = count++;
        }
        for(; col > startY; col--) {//从右到左，填充下边界
            res[row][col] = count++;
        }
        for(; row > startX; row--) {//从下到上，填充左边界
            res[row][col] = count++;
        }
        startX++;
        startY++;
        offset++;
    }
    if(n % 2==1) res[mid][mid] = count;
    return res;
}
```