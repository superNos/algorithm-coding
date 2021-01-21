
## 包含min函数的栈
**题目描述**

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

```javascript
function push(node)
{
    // write code here
}
function pop()
{
    // write code here
}
function top()
{
    // write code here
}
function min()
{
    // write code here
}
```

**思路**

按上右下左的顺序进行遍历，定义四个遍历标记矩阵行和列的首尾，<br>
上边遍历完，行的开始标记向下移一位，<br>
右边遍历完，列的结尾标记向左移一位，<br>
下边遍历完，行的结尾标记向上移一位，<br>
左边遍历完，列的开始标记向右移一位，<br>
直至两个开始标记都大于结尾标记，注意判断边界