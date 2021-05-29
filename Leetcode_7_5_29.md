题目：
给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。
假设环境不允许存储 64 位整数（有符号或无符号）。

1.

```
class Solution {
    public int reverse(int x) {
        int rev=0;
        while(x!=0){
            int b=x%10;
            x/=10;
        if(rev>214748364||rev<-214748364)
        {
            return 0;
        }
            rev=rev*10+b;
        }        
    return rev;
    }
}
```

int 的范围是 [-2^{31} ,2^{31}-1][−231,231−1] 也就是 [-2147483648,2147483647][−2147483648,2147483647] 。明显 9646324351 超出了范围，造成了溢出。所以我们需要在输出前，判断是否溢出。

问题的关键就是下边的一句了。

rev = rev * 10 + pop;

为了区分两个 rev ，更好的说明，我们引入 temp 。

temp = rev * 10 + pop;

rev = temp;

我们对 temp = rev * 10 + pop; 进行讨论。intMAX = 2147483647 , intMin = - 2147483648 。

对于大于 intMax 的讨论，此时 x 一定是正数，pop 也是正数。

- 如果 rev > intMax / 10 ，那么没的说，此时肯定溢出了。
- 如果 rev == intMax / 10 = 2147483647 / 10 = 214748364 ，此时 rev * 10 就是 2147483640 如果 pop 大于 7 ，那么就一定溢出了。但是！如果假设 pop 等于 8，那么意味着原数 x 是 8463847412 了，输入的是 int ，而此时是溢出的状态，所以不可能输入，所以意味着 pop 不可能大于 7 ，也就意味着 rev == intMax / 10 时不会造成溢出。
- 如果 rev < intMax / 10 ，意味着 rev 最大是 214748363 ， rev * 10 就是 2147483630 , 此时再加上 pop ，一定不会溢出。

对于小于 intMin 的讨论同理。

```java
public int reverse(int x) {
    int rev = 0;
    while (x != 0) {
        int pop = x % 10;
        x /= 10;
        if (rev > Integer.MAX_VALUE/10 ) return 0;
        if (rev < Integer.MIN_VALUE/10 ) return 0;
        rev = rev * 10 + pop;
    }
    return rev;
}
Copy
```

时间复杂度：循环多少次呢？数字有多少位，就循环多少次，也就是 log_{10}(x) + 1*l**o**g*10(*x*)+1 次，所以时间复杂度是 O（log（x））。

空间复杂度：O（1）。

当然我们可以不用思考那么多，用一种偷懒的方式 AC ，我们直接把 rev 定义成 long ，然后输出前判断 rev 是不是在范围内，不在的话直接输出 0 。

```java
public int reverse(int x) {
    long rev = 0;
    while (x != 0) {
        int pop = x % 10;
        x /= 10;
        rev = rev * 10 + pop;
    }
    if (rev > Integer.MAX_VALUE || rev < Integer.MIN_VALUE ) return 0;
    return (int)rev;
}
```