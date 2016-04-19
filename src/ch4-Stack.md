
# 栈 Stack

* **LIFO**: last in first out

```javascript

interface IStack {
    // 数据储存
    dataStore: Array<any>,
    // 栈顶指针
    top: number,

    // 入栈
    push(elem: any): any,
    // 出栈
    pop(): any,

    // 返回栈顶元素
    peek(): any,

    // 返回栈内元素数量
    length(): number,

    // 清空栈
    clear(): Array<any>,

    // 栈是否为空
    isEmpty(): boolean
};


class Stack implements IStack {
    top: number;
    dataStore: Array<any>;

    constructor(...args) {
        this.top = args.length;
        this.dataStore = args;
    }

    push(elem: any): any {
        return (this.dataStore[this.top++] = elem);
    }

    pop(): any {
        this.top--;
        return this.dataStore.pop();
    }

    peek(): any {
        return this.dataStore[this.top - 1];
    }

    length(): number {
        return this.top;
    }

    clear(): Array<any> {
        this.top = 0;
        return this.dataStore.slice(0);
    }

    isEmpty(): boolean {
        return this.top <= 0;
    }
}

```

## 2~9 进制转换

```javascript

function mulBase(num, base) {
    var stack = new Stack();

    do {
        stack.push(num % base);
        num = Math.floor(num / base);
    } while (num > 0);
    
    var converted = '';
    while (stack.length() > 0) {
        converted += stack.pop();
    }
    return converted;
}

```


## 【小插曲】

最近在看js函数式编程，突然想到, 这里用**递归**怎么实现？

```javascript

function mulBase(num, base) {
    return _mulBase(num, base, '');

    function _mulBase(num, base, str) {
        str = str || '';

        if (num <= 0) {
            return str;
        }
        
        str = num % base + str;
        num = Math.floor(num / base);

        // 关于尾调用和尾递归  参考阮大神的叙述
        // @see http://es6.ruanyifeng.com/#docs/function#尾调用优化
        return _mulBase(num, base, str);
    }
}

```

 

