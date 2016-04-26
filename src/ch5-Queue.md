
# 队列 Queue

* **FIFO**: first in first out

```javascript

interface IQueue {
    // 数据储存
    dataStore: Array<any>,

    // 入队
    enqueue(elem: any): any,

    // 出队
    dequeue(): any,

    // 返回队首元素
    front(): any,

    //返回队尾元素
    back(): any,

    length(): numbe,

    // 队是否为空
    isEmpty(): boolean
};

class Queue implements IQueue {
    dataStore: Array<any>;

    constructor(...args) {
        this.dataStore = args;
    }

    enqueue(elem: any): any {
        return this.dataStore.push(elem);
    }

    dequeue(): any {
        return this.dataStore.shift();
    }

    front(): any {
        return this.dataStore[0];
    }

    back(): any {
        return this.dataStore[this.dataStore.length - 1];
    }

    length() {
        return this.dataStore.length;
    }

    isEmpty(): boolean {
        return this.dataStore.length <= 0;
    }
}

```

## 0-99 之间数字的**基数排序**

- 未封装的版本

```javascript

var nums = [91, 46, 85, 15, 92, 35, 31, 22];
var queues = [];
// 生成队列
for (let i = 0; i < 10; i++) {
    queues[i] = new Queue();
}

// 对个位数进行排序
for (let i = 0, len = nums.length; i < len; i++) {
    let num = nums[i];
    let queueAt = (num % 10) | 0;
    queues[queueAt].enqueue(num);
}

for (let j = 0, i = 0; j < 10; j++) {
    let queue = queues[j]
    while (!queue.isEmpty()) {
        nums[i++] = queue.dequeue();
    }
}

// 对十位进行排序
for (let i = 0, len = nums.length; i < len; i++) {
    let num = nums[i];
    let queueAt = (num / 10) | 0;
    queues[queueAt].enqueue(num);
}

for (let j = 0, i = 0; j < 10; j++) {
    let queue = queues[j];
    while (!queue.isEmpty()) {
        nums[i++] = queue.dequeue();
    }
}

// [15, 22, 31, 35, 46, 85, 91, 92]
console.log(nums);

```

- 封装后

```javascript

// ...

distributeAndCollect(nums, queues, 1);
distributeAndCollect(nums, queues, 2);

function distributeAndCollect(nums, queues, digit) {
    for (let i = 0, len = nums.length; i < len; i++) {
        // 用个黑办法获取数字
        let num = nums[i] + '',
            queueAt = num[num.length - digit] || 0;

        queues[queueAt].enqueue(num | 0);
    }

    for (let j = 0, i = 0; j < 10; j++) {
        let queue = queues[j];
        while (!queue.isEmpty()) {
            nums[i++] = queue.dequeue();
        }
    }
}

```
 
- 再次封装后(还是只能针对正整数)

若再修改下，应该能够将适用范围拓展到所有整数...

```javascript

var nums = [1, 45, 22, 2984, 21228, 124, 844, 62];

baseSort(nums);

function distributeAndCollect() {
    // .....
}

function baseSort(nums) {
    // 生成队列
    for (let i = 0; i < 10; i++) {
        queues[i] = new Queue();
    }

    let max = Math.max.apply(Math, nums),
        maxDigit = (max + '').length,
        digit = 1;

    while (digit <= maxDigit) {
        distributeAndCollect(nums, queues, digit);
        digit += 1;
    }

    return nums;
}

```


## 优先队列

```javascript

// ...

@override
dequeue(): any {
	let entry = 0;

	let dataStore = this.dataStore;
	for (let i = 1, len = dataStore.len; i < len; i++) {
		if (dataStore[i].priority < dataStore[entry].priority) {
			entry = i;
		}
	}

    return this.dataStore.splice(entry, 1);
}

// ...

```