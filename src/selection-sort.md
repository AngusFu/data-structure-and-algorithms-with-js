 ```javascript
 
// 选择排序
function selectionSort(arr) {
  arr = arr.slice(0);
  var len = arr.length;
  var i = 0;
  var j = 0;
  var minIndex = 0;
  var temp = 0;

  for (i = 0; i < len - 1; i++) {
    // 将当前的数字与后面子序列中最小数进行换位
    // 这样每次拿到前面的都是最小的数字
    minIndex = i;

    // 寻找子序列中最小数的索引
    // 每一轮得比较 n - i 次
    for (j = i + 1; j < len; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    // 如果当前数比后面子序列最小元素大
    // 则进行换位处理
    if (minIndex !== i) {
      temp = arr[i];
      arr[i] = arr[minIndex];
      arr[minIndex] = temp;
    }
  }
  return arr;
}

selectionSort(arr);
```
