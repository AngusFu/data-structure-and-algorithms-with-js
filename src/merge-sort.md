```javascript

// 归并排序
// 分治法 递归
// 将问题化小
var merge = function(left, right) {
  let temp = [];
  // 比较
  var i = 0;
  var j = 0;
  var llen = left.length;
  var rlen = right.length;

  /*
    []               <= [1, 2, 5]   [3, 4, 7, 8, 20]
    [1]              <= [2, 5]      [3, 4, 7, 8, 20]
    [1, 2]           <= [5]         [3, 4, 7, 8, 20]
    [1, 2, 3]        <= [5]         [4, 8, 20]
    [1, 2, 3, 4]     <= [5]         [8, 20]
    [1, 2, 3, 4, 5]  <= []          [8, 20]

    result:
    [1, 2, 3, 4, 5, 8, 20] 
  */

  // 将其中一个数组穷尽
  // 另外一个数组剩下的肯定都是比当前所有数都大的
  while (i < llen && j < rlen) { 
    temp.push(left[i] > right[j] ? right[j++] : left[i++]);
  }

  return temp.concat(left.slice(i)).concat(right.slice(j));
};

function mergeSort(arr) {
  arr = arr.slice(0);
  var len = arr.length;
  if (len === 1) return arr;

  var mid = Math.ceil(len / 2);

  return merge(
    mergeSort(arr.slice(0, mid)),
    mergeSort(arr.slice(mid, len)) 
  );
}

console.log(mergeSort([22, 11, 33, 8, 88, 1, 37, 189, 23, 5]));
```
