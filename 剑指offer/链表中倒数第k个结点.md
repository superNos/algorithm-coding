## 链表中倒数第k个结点
**题目描述**

输入一个链表，输出该链表中倒数第k个结点。

```javascript
    /*function ListNode(x){
        this.val = x;
        this.next = null;
    }*/
    function FindKthToTail(head, k)
    {
        let flag = JSON.parse(JSON.stringify(head));
        let length = 0;
        while(flag) {
            length ++;
            flag = flag.next;
        }
        if(k > length) return null
        length -= k;
        while(length) {
            head = head.next;
            length --;
        }
        return head
    }
```

**思路** <br>
先查出链表长度，然后返回第`长度-k`个节点即可，注意如何k>总长度时，需要返回null
