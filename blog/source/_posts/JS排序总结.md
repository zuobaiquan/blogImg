---
title: JS排序总结
date: 2017-03-21 16:01:49
tags: JavaScript
---

两路快排：
<!--more-->
```javascript
function partion(arr, low, high){
   var idx = low;
   var pivot = arr[low];
   while(low<high){
      while(low<high && arr[high]>= pivot){ high--; }
      while(low<high && arr[low] <= pivot) { low++; }
      if(low<high){
         var temp = arr[high];
         arr[high] = arr[low];
         arr[low] = temp;
      }
   }
   if(low == high){
     arr[idx] = arr[low];
     arr[low] = pivot;
   }
   return low;
}

function quicksort1(arr, low, high){
  if(low < high ){
     var pivot = partion(arr, low, high);
     quicksort(arr, low, pivot-1);
     quicksort(arr, pivot+1, high);
  }
}

function quicksort2(arr, low, high){
   var stack = [];
   if(low<high){
     var mid = partion(arr, low, high);
     if(low< mid -1){
       stack.push(low);
       stack.push(mid-1);
     }
     if(mid+1< high){
       stack.push(mid+1);
       stack.push(high);
     }
   }

    while(stack.length > 0){
      var higher = stack.pop();
      var lower = stack.pop();
      var midder = partion(arr, lower, higher);
      if(lower < midder -1){
         stack.push(lower);
         stack.push(midder -1);
      }
      if(midder+1 < higher){
         stack.push(midder + 1);
         stack.push(higher);
      }
    }

}

var arr = [3,6,2,9,4,7];
quicksort1(arr, 0, arr.length -1);
quicksort2(arr, 0, arr.length -1);
```

冒泡排序：优化后的

```javascript
function Bubblesort(arr){
  var len = arr.length;
  for(var i=0;i< len-1; i++){ //代表要排序多少次
    for(var j=0;j< len-i-1;j++){ //每次的起始和截止位置
      if(arr[j] > arr[j+1]){
         var tem = arr[j];
         arr[j] = arr[j+1];
         arr[j+1] = tem;
      }  
    }
  }
}
```

选择排序：

```javascript
function Selection(arr){
   for(var i=0;i< arr.length-1; i++){ //代表要排序多少次
     for(var j=i+1; j<arr.length; j++){ //起始和截止位置
        if(arr[i] > arr[j]){
           var temp = arr[i];
           arr[i] = arr[j];
           arr[j] = temp;
        }
     }
   }
}
```

插入排序：一般的插入排序

对于每个未排序数，在已排序序列中从后向前扫描找到相应位置并插入。默认arr[0]为开始。

```javascript
function InsertSort(arr){
   for(var i=1;i< arr.length;i++){ //需要对arr.length-1个数进行排序，级进行这么多次
     var item = arr[i]; //记录待排序数数值和下标
     var pos = i;
     while(i>0 && item< arr[i-1]){ //找应该插在哪个位置
        i--;
     }
     //位置已确定，即从i位置往后移动
     for(var k=pos; k>i; k--){
       arr[k] = arr[k-1];
     }
     arr[k] = item;
   }
}
```

存在缺陷：我在查找应该插入哪个位置的时候只是单纯的去找位置，找到后才移动，可以更为优化，即在查找的时候若不是就移动一个

```javascript
function InsertSort(arr){
   for(var i=1;i< arr.length;i++){
     var item = arr[i];
     var pos = i;
     while(i>0 && item< arr[i-1]){
        arr[i] = arr[i-1];
        i--;
     }
     arr[i] = item;
   }
}
```

希尔排序：分组插入排序（高级插入排序）

第一次排序：将数组按增量划分为多个列，装在一个表中，对列分别进行插入排序，之后再合并为一个数组
第二次排序：将数组按另一个增量划分多个列，同上

```javascript
function shellSort(arr){
var gap = Math.floor(arr.length/2); 
while(gap>0){
  for(var i=gap; i<arr.length; i++){
     var temp = arr[i];
     while(i>=gap && temp < arr[i-gap]){
       arr[i] = arr[i-gap];
       i -= gap;
     }
     arr[i] = temp;
  }
  gap = Math.floor(gap/2);
  console.log(gap)
 }
}
```

归并排序：

有点问题：

```javascript
function dev(arr){
  if(arr.length <=1) return arr;
  var mid = Math.floor(arr.length/2);
  var leftarr = dev(arr.slice(0, mid));
  var rightarr = dev(arr.slice(mid));
  return merge(leftarr, rightarr);
}

function merge(leftarr, rightarr){ 
  var l,r = 0;
  var result = [];
  while(l<leftarr.length && r< rightarr.length){
    if(leftarr[l] < rightarr[r]){
      result.push(leftarr[l]);
      l++
    }else{
      result.push(rightarr[r]);
      r++;
    }
  }
  for(var i=l; i< leftarr.length; i++){
     result.push(leftarr[i]);
  }
  for(var i=r; i< rightarr.length; i++){
     result.push(rightarr[i]);
  }
  return result;
}
```

二分排序：

```javascript
function binarySearch(value,arr,startIndex,endIndex) {
    if(!value|| !(arr instanceof Array)) return;
        var midIndex= Math.floor((startIndex + endIndex)/2),
        midval = arr[midIndex];
    if(midval === value){
        return midIndex;
    }else if (midval > value) {
       return binarySearch(value, arr, startIndex, midIndex - 1);
    }else {
       return binarySearch(value, arr, midIndex + 1, endIndex);
    }
}
```



