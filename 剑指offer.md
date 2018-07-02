# 剑指offer

标签（空格分隔）： 秋招 笔试 java 练手

---

### 替换空格
    题目描述
    请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

第一个版本

 - 未实现在原字符串上的直接修改（会报数组越界）。新建了一个字符串s1
 - 从后向前替换，避免多个空格时，后面的字符会移动多次的情况，每个字符只需移动一次
 - 不考虑java里面的replace函数


```java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        int count = 0;
        char[] s = str.toString().toCharArray();
        
        for(int i=0;i<s.length;i++)
        {
            if(s[i]==' '){
                count++;
            }
         }
        char[] s1 = new char[2*count + str.length()];
        int loc=2*count + str.length()-1;
        for(int i=s.length-1;i>=0;i--)
        {
            if(s[i]!=' ')
            {
                s1[i+count*2]=s[i];
            }
                else
                {   count--;
                    s1[i+2*count]='%';
                    s1[i+count*2+1]='2';
                    s1[i+count*2+2]='0';
                    
                }
        }
    	 return String.valueOf(s1);
    }
}
```

### 从尾到头打印链表
    题目描述
    输入一个链表，从尾到头打印链表每个节点的值。
后进先出，翻转，联想到堆栈

 - 利用堆栈先进后出的特性，链表的头先进则最后出，即将链表翻转，实现从尾到头
 - 还有递归解法

```java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
         Stack<Integer> stack=new Stack<Integer>();
        while(listNode!=null){
            stack.push(listNode.val);
            listNode=listNode.next;
        }
        ArrayList<Integer> list=new ArrayList<Integer>();
        while(!stack.isEmpty())
        {
            list.add(stack.pop());
        }
        return list;
    }
}
```

### 重建二叉树
    题目描述
    输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍    历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}    和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。