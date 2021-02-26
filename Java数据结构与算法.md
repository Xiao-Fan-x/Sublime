## 斐波那契实现数组相加

```java
public class Fibona {
    public static void main(String[] args) {
        int[] a = {2,5,3,9,12,7};

        int sum = f(a,0);
        System.out.println(sum);
    }

    private static int f(int[] a, int i) {
        if (i==a.length-1){
            return a[i];
        }else {
            return a[i]+f(a,i+1);
        }
    }
}
```

## 尼姆问题(Nimm)

​       有两堆石子，有两个绝顶聪明的人在玩一个游戏，每次每个人可以从一堆石子中取任意数量但不少于1个的石子，或从两堆中同时取走相同数量的石子，最后一个取完石子的人获胜。







## 整数的划分问题

对于正整数n=6，可以分划为： 

6 

5+1 

4+2, 4+1+1 

3+3, 3+2+1, 3+1+1+1 

2+2+2, 2+2+1+1, 2+1+1+1+1 

1+1+1+1+1+1+1 

