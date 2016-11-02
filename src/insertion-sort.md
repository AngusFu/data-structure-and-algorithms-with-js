```javascript
var arr = [22, 11, 33, 8, 88, 1, 37, 189, 23, 5];

// 插入排序
// 类似扑克牌
var insertionSort = (arr) => {
  arr = arr.slice(0);

  var i = 0;
  var j = 0;
  var temp = 0;
  var len = arr.length;
  var final = 0;

  for (i = 1; i < len; i++) {
    // 当前要向前比较的数字
    temp = arr[i];
    
    // 从当前数倒着往前数
    // 一一比较，直到找到倒数最后一个比当前数大的为止
    j = i - 1;
    final = j;

    // 当前数字前面子序列是已经排序好的
    // 我们的目标是找到最后一个比当前数要大的数字
    // 在这个过程中，所有比当前数大的都得往后挪动一位
    // j 最后的值就是 j 应该存放的位置
    while (j >= 0 && arr[j] > temp) {
      // 向后移动
      arr[j + 1] = arr[j];         
      final = j;
      j--;
    }
    // 最后将当前数入位
    arr[final] = temp;
  }

  return arr;
};

insertionSort(arr);
 ```
