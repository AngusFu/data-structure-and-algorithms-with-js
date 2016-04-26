
# 链表 LinkedList

## 基于对象的链表

```javascript

class LNode {
    element: any;
    next: any;

    constructor(elem) {
        this.element = elem;
        this.next = null;
    }
}

class LinkedList {
    head: LNode;

    constructor() {
        this.head = new LNode('head');
    }

    find(item: any): LNode {
        var curNode = this.head;
        while (curNode.element !== item) {
            curNode = curNode.next;
        }
        return curNode;
    }

    findPrev(item: any): LNode {
        var curNode: LNode = this.head;

        while (curNode.next && curNode.next.element !== item) {
            curNode = curNode.next;
        }

        return curNode;
    }

    insert(newElem: any, item: any): LNode {
        var newNode: LNode = new LNode(newElem);
        var curNode: LNode = this.find(item);
        newNode.next = curNode.next;
        curNode.next = newNode;

        return newNode;
    }

    remove(item: any): void {
        var prevNode: LNode = this.findPrev(item);

        if (prevNode && prevNode.next) {
            prevNode.next = prevNode.next.next;
        }
        prevNode = null;
    }

    display(): string {
        var curNode: LNode = this.head;
        var str: string = '';

        while (curNode) {
            str += ('' + curNode.element) + "  ==>  ";
            console.log(curNode.element);
            curNode = curNode.next;
        }

        return str;
    }
}


```