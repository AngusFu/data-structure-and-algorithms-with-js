# 数组 Arrays

## 2.6 二维数组和多维数组 (Matrix)

```javascript

Array.matrix = function (rows, cols, defaultVal) {
    var arr = [],
        i = 0,
        j = 0,
        columns = null,
        usePrimaryVal = typeof defaultVal !== 'function';

    for (i = 0; i < rows; i++) {
        columns = [];

        for (j = 0; j < cols; j++)  {
            columns[j] = usePrimaryVal && defaultVal || defaultVal(i, j);
        }

        arr[i] = columns;
    }

    return arr;
};

// test 1
var matrix_test_1 = Array.matrix(9, 9, 100);

// test 2
var matrix_test_2 = Array.matrix(9, 9, (i, j) => {
    return `[${i} , ${j}]`;
});

```