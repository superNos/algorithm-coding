
## 数组中出现次数超过一半的数字

**题目描述**

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

```javascript
    function GetLeastNumbers_Solution(input, k)
    {
        let arr = Array.from(new Set([...input]))
        if(k > arr.length) return []
        return arr.sort((a, b) => a - b).splice(0,k)
    }
```

**思路**

