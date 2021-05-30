题目：![image-20210530211425775](C:\Users\86135\AppData\Roaming\Typora\typora-user-images\image-20210530211425775.png)

1.题目比较简单，想到直接遍历

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        for(int i=0;i<32;i++){
            if(Math.pow(2,i)==n)
                return true;
        }
        return false;
    }
}
```

其中Math.pow是Math自带的方法，pow（double a,double b）需要注意它的参数是double类型表示为a的b次方，但题目进阶为不使用循环/递归解决。

2.看了题解的一个很厉害的方法

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
}
```

![image-20210530212010388](C:\Users\86135\AppData\Roaming\Typora\typora-user-images\image-20210530212010388.png)

按位与&运算： 两位同时为1才为1，否则为0；

按位|运算: 	一个为1结果就为1；

异或与^:	不同为1，否则为0（可理解为相加不进位）

这种思路非常厉害，深刻的利用了&运算的特性，也对2的n次方的数有了解，知道生成的数二进制最高位为1，其余为0，这需要我们有细心观察的能力