1. 给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

   如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

   您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

   > ```
   > 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
   > 输出：7 -> 0 -> 8
   > 原因：342 + 465 = 807
   > ```

   ```javascript
   // 业务代码
   var addTwoNumbers = function(l1, l2) {
       let num1 = parseInt((l1.reverse()).join(''))
       let num2 = parseInt((l2.reverse()).join(''))
       let sum = num1 + num2
       let arr = String(sum).split('')
       return arr.reverse()
   };
   // 
   ```

   