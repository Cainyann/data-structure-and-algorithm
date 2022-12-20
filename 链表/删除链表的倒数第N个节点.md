
[删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)


>给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。
>进阶：你能尝试使用一趟扫描实现吗？
>输入：head = [1,2,3,4,5], n = 2 输出：[1,2,3,5] 示例 2：
   输入：head = [1], n = 1 输出：[] 



- 关键词：倒数第n个 + 一趟遍历

- 标签：快慢指针 /  栈
- 思路
	1. 假设总节点个数为4，倒数第2个就是正数第3个，总结点为L，倒数第n个就是正数第L-n+1个！一趟遍历可以解决！
	2. 双指针：快慢指针
- 注意：
	1. 走到第n个节点只要走n-1步，for循环里`i从0开始`，`i<n`
	 `for(let i=0;i<n;i++){cur = cur.next}`
	 2. 删除第n个节点，要走到第n-1个



>[!summary]
>hhhh


>[!note]
>hhh

>[!danger]
>hhhh

>[!tip]
>hhhh

>[!example]
>hhh

>[!todo]
>hhh

>[!attention]
>hhh

>[!cite]
>hhh

>[!FAQ]- toggle to see
>hhh







## 方法一
>计算链表长度


>[!tip]
>删除倒数第n个节点，从虚拟头节点开始走到需要目标节点的前一个节点，要走length-n步



```javascript
var removeNthFromEnd = function(head, n) {
    //先获取长度
    const getLength = function(headNode){
        let len = 0;
        while(headNode){
            len ++
            headNode = headNode.next
        }
        return len
    }
    //倒数第n个，就是正数第len-n+1个
    //要删除第len-n+1个节点，要走到前一个也就是第len-n个节点
    //从dummy开始走，要走len-n-1+1步
    const len = getLength(head)
    let dummy = new ListNode(0,head)
    let cur = dummy //使用虚拟头节点，便于处理head为null的情况，返回dummy.nexy就行
    for(let i=1;i<len-n+1;i++){
        cur = cur.next
    }
    cur.next = cur.next.next //删除节点
    return dummy.next
};
```


## 方法二
>[!tip]
>都从dummy出发，fast先走n步再同时开始走，则fast走到尾巴节点时，slow恰好走到要删除的节点的前一个
```javascript
var removeNthFromEnd = function(head, n) {
   //快慢指针
   //删除一个节点就要找到他的上一个节点
   //走到倒数第n个节点的上一个节点就是从尾巴往前走n步
   //设置dummy，从dummy走到尾巴节点视为结束，共要走length步
   //都从dummy出发，fast先走n步再同时开始走，则fast走到尾巴节点时，slow恰好走到要删除的节点的前一个
   const dummy = new ListNode(0,head)
   let slow = dummy,fast = dummy
   for(let i=0;i<n;i++){
       fast = fast.next
   }
   while(fast.next){
       fast = fast.next
       slow = slow.next
   }
   //删除
   slow.next = slow.next.next
   return dummy.next
};
```



## 相关题目
