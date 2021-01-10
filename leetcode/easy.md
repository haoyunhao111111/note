1. 编写一个函数来查找字符串数组中的最长公共前缀。如果不存在公共前缀，返回空字符串 `""`。

   ```javascript
   // 暴力循环
   var longestCommonPrefix = function(strs) {
     if(!strs.lenth) return ""
     strs.sort()
     for (let i= strs[0].length;i>0;i--) {
       let str = strs[1].slice(0,i)
       let index = strs.every(item => item.slice(0,i) === str)?i:0
       if (index) return strs[0].slice(0,index)
     }
     return ''
   }
   console.log(longestCommonPrefix(['abcd', 'abc']))
   // 内耗低，效率高
   var longestCommonPrefix = function (strs) {
     strs.sort()//按编码排序
     if (strs.length === 0) return ''//空数组返回''
     var first = strs[0],
       end = strs[strs.length - 1]
     if (first === end || end.match(eval('/^' + first + '/'))) {
       return first//first包含于end返回first
     }
     for (var i = 0; i < first.length; i++) {
       if (first[i] !== end[i]) {
         return first.substring(0, i)//匹配失败时返回相应字符串
       }
     }
   };
   console.log(longestCommonPrefix(['abcd', 'aabc']))
   ```

   