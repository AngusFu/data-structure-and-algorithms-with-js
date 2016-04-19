# 列表 Lists

## ES6 实现

```javascript

interface IList {
    listSize: number,
    pos: number,
    dataStore: Array<any>,

    // 数组字符串形式
    toString(): string,

    // 清空列表
    clear(): Array<any>,

    // 查找元素
    find(elem: any): number,

    // 列表是否包含元素
    contains(elem: any) : boolean,

    // 插入元素
    insert(elem: any, after: any): any,

    // 列表尾部添加元素
    append(elem: any): any,

    // 删除元素
    remove(elem: any): any,

    // 设置列表位置指针到头部
    front(): number,

    // 设置列表位置指针到尾部部
    end(): number,

    // 列表当前位置移动
    moveTo(pos: number): number,

    // 列表位置指针前移
    prev(): number,

    // 列表位置指针后移
    next(): number,

    // 列表当前位置是否是最后
    hasNext(): boolean,

    // 列表当前位置是否是最前
    hasPrev(): boolean,

    // 获取列表元素长度
    length(): number,

    // 列表当前位置
    currentPos(): number,

    // 返回列表当前位置的元素
    getElement(): any

};

class List implements IList {
    listSize: number;
    pos: number;
    dataStore: Array<any>;

    /**
     * @constructor
     */
    constructor(...args) {
        this.listSize = args.length;
        this.pos = 0;
        this.dataStore = args;
    }


    /**
     * @override
     *
     * 数组字符串形式
     * @return {String}
     */
    toString(): string {
        // TODO
        return this.dataStore.toString();
    }


    /**
     * 清空列表
     */
    clear(): Array<any> {
        let temp = this.dataStore;

        this.listSize  = 0;
        this.pos = 0;
        this.dataStore = [];
        return temp;
    }


    /**
     * 查找元素
     * @param  {Any} elem 查找的元素
     * @return {Number}  元素的位置
     */
    find(elem: any): number {
        return +this.dataStore.indexOf(elem);
    }


    /**
     * 列表是否包含元素
     * @param  {Any} elem 查找的元素
     * @return {Boolean}
     */
    contains(elem: any): boolean {
        // return !!~this.find(elem);
        return this.find(elem) > -1;
    }

    /**
     * 插入元素
     * @param  {Any}    elem  要插入的元素
     * @param  {Any}    after 插在哪个元素后面
     * @return {Any}          返回插入的元素
     */
    insert(elem: any, after: any): any {
        let insertPos: number = this.find(after);

        if (insertPos < 0) {
            throw 'after element is not a valid element in this list';
        }

        this.dataStore.splice(insertPos + 1, 0, elem);
        this.listSize += 1;

        return elem;
    }


    /**
     * 列表尾部添加元素
     * @return {Any}  返回插入的元素
     */
    append(elem: any): any {
        return this.dataStore[this.listSize++] = elem;
    }


    /**
     * 删除元素
     * @return {Any}  返回被删除的元素
     */
    remove(elem: any): any {
        let elemPos = this.find(elem);

        if (elemPos < 0) {
            throw 'element to be removed is not a valid element in this list';
        }

        this.dataStore.splice(elemPos, 1);
        this.listSize -= 1;

        return elem;
    }


    /**
     * 设置列表位置指针到头部
     * @return {Number}  返回位置指针
     */
    front(): number {
        return this.pos = 0;
    }


    /**
     * 设置列表位置指针到尾部部
     * @return {Number}  返回位置指针
     */
    end(): number {
        return this.pos = this.listSize - 1;
    }


    /**
     * 列表当前位置移动
     * @param {Number}   pos   当前位置移动到的地方
     * @return {Number}  返回移动后的位置
     */
    moveTo(pos: number): number {
        return this.pos = +pos || 0;
    }


    /**
     * 列表位置指针前移
     * @return {Number}  返回位置指针
     */
    prev(): number {
        return --this.pos;
    }


    /**
     * 列表位置指针后移
     * @return {Number}  返回位置指针
     */
    next(): number {
        return this.pos < this.listSize && (++this.pos) || this.pos;
    }


    /**
     * 列表当前位置是否是最后
     * @return {Boolean}
     */
    hasNext(): boolean {
        return this.pos < this.listSize;
    }


    /**
     * 列表当前位置是否是最前
     * @return {Boolean}
     */
    hasPrev(): boolean {
        return this.pos >= 0;
    }


    /**
     * 获取列表元素长度
     * @return {Number}
     */
    length(): number {
        return this.listSize;
    }

    /**
     * 列表当前位置
     * @return {Number}
     */
    currentPos(): number {
        return this.pos;
    }


    /**
     * 返回列表当前位置的元素
     * @return {Any}
     */
    getElement(): any {
        return this.dataStore[this.pos];
    }
}


```

## 使用迭代器访问列表

```javascript

let list = new List(1, 2, 3, 4, 5, 6, 7);

// 1 正序
for (list.front(); list.hasNext(); list.next()) {
    console.log(list.getElement());
}

// 2 逆序
for (list.end(); list.hasPrev(); list.prev()) {
    console.log(list.getElement());
}

```


## 让人联想到 ES6 的 ``Iterator`` 和 ``for...of``

关于``Iterator`` 和 ``for...of`` 详细情况，还是参考阮大神的开源作品《ECMAScript 6 入门》之[Iterator和for...of循环](http://es6.ruanyifeng.com/#docs/iterator)。

```javascript

class List {
    constructor(...args) {
        this.pos = 0;
        this.dataSource = args;
        this.listSize = args.length;
    }

    [Symbol.iterator]() { return this; }

    next() {
        var value = this.dataSource[this.pos];
        var done  = this.pos > this.listSize - 1;
        this.pos += 1;
        return { value, done};
    }
}

```

