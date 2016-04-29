---
title: some interview questions
date: 2016-04-16 10:10:01
tags: 
  - interview
  - algorithm
  - javascript
  - network
---
> 非前端部分

### 数组求交集

```js
Set.prototype.intersection = function(otherSet) {
  let rstSet = new Set();
  let originValues = [...this.values()];
  for (let value of originValues) {
    if (otherSet.has(value)) rstSet.add(value) 
  }
  return rstSet;
}
let arr1 = [1, 2, 3];
let arr2 = [2, 3, 4];
console.log(...[new Set(arr1).intersection(new Set(arr2))]);
```

### 数组去重
```js
Array.prototype.getUnique = function(){
   var u = {}, a = [];
   for(var i = 0, l = this.length; i < l; ++i){
      if(u.hasOwnProperty(this[i])) {
         continue;
      }
      a.push(this[i]);
      u[this[i]] = 1;
   }
   return a;
}
```

```js
Array.prototype.getUnique = function(){
    return this.filter((value, index, self) => 
        self.indexOf(value) === index
    )
}
```

```js
Array.prototype.getUnique = function(){
    return [...new Set(this)];
}
```

### TCP 三次握手，四次挥手
![image](http://hi.csdn.net/attachment/201108/7/0_1312718352k8l6.gif)

![image](http://hi.csdn.net/attachment/201108/7/0_1312718564tZXD.gif)
### TCP 滑动窗口
发送和接受方都会维护一个数据帧的序列，这个序列被称作窗口。发送方的窗口大小由接受方确定，目的在于控制发送速度，以免接受方的缓存不够大，而导致溢出，同时控制流量也可以避免网络拥塞。下面图中的4,5,6号数据帧已经被发送出去，但是未收到关联的ACK，7,8,9帧则是等待发送。可以看出发送端的窗口大小为6，这是由接受端告知的（事实上必须考虑拥塞窗口cwnd，这里暂且考虑cwnd>rwnd）。此时如果发送端收到4号ACK，则窗口的左边缘向右收缩，窗口的右边缘则向右扩展，此时窗口就向前“滑动了”，即数据帧10也可以被发送。
![image](http://blog.csdn.net/images/blog_csdn_net/dotjox/slidingwindow.jpg)

### TCP 拥塞控制
WIP

### socket 模型
[socket阻塞与非阻塞，同步与异步、I/O模型](http://blog.csdn.net/hguisu/article/details/7453390)

### 大整数加、减、乘、除、求模运算实现


### 很多整数，找其中出现次数最多的那个数

### 二分查找
```js
function binarySearch (sortedArr, item) {
  let low = 0, high = sortedArr.length - 1;
  while (low <= high) {
    let mid = Math.floor((high - low) / 2);
    if (sortedArr[mid] === item) return mid;
    if (sortedArr[mid] > item) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return -1;
}
```

### 快速排序
```js
var quickSort = function (arr) {
  let pivot = Math.floor(arr.length / 2);
  let left = [], right = []
  for (let value of arr) {
    value < pivot ? left.concat(value) : right.concat(value);
  }
  return quickSort(left).concat(pivot, quickSort(right))
}
```
### 归并排序
```js
Array.prototype.mergeSort = function () {
  return mergeRec(this);
}
function mergeRec (arr) {
  if (arr.length === 1) return arr;
  let mid = Math.floor(arr / 2);
  let left = arr.slice(0, mid);
  let right = arr.slice(mid);
  return merge(mergeRec(left), mergeRec(right));
}
function merge(arr1, arr2) {
  let i = 0, j = 0;
  let rst = [];
  while(i < arr1.length && j < arr2.length) {
    arr1[i] < arr2[j] ? rst.push(arr1[i++]) : rst.push(arr2[j++]);
  }
  return rst.concat(arr1.slice(i), arr2.slice(j))
}
```
### 判断链表是否有环
 2 指针，一个slow, 一个fast，是否重合
### 红黑树性质

### 最大公约数
```js
function gcd(a, b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}
```

### 进程调度算法
[http://blog.csdn.net/wanghao109/article/details/13004507](http://blog.csdn.net/wanghao109/article/details/13004507)
