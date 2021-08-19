# 排序

插入排序、希尔排序、选择排序、堆排序、冒泡排序、快速排序、

归并排序、计数排序、桶排序

冒泡排序，选择排序，插入排序，快速排序，堆排序，归并排序，希尔排序，桶排序，基数排序新年帮您排忧解难。有向图，无向图，有环图，无环图，完全图，稠密图，稀疏图，拓扑图祝您新年宏图大展。最长路，最短路，单源路径，所有节点对路径祝您新年路路通畅。二叉树，红黑树，van
Emde
Boas树，最小生成树祝您新年好运枝繁叶茂。最大流，网络流，标准输入流，标准输出流，文件输入流，文件输出流祝您新年顺顺流流。线性动规，区间动规，坐标动规，背包动规，树型动归为您的新年规划精彩。散列表，哈希表，邻接表，双向链表，循环链表帮您在新年表达喜悦。O(
1), O(log n), O(n), O(nlog n), O(n^2), O(n^3), O(2^n), O(n!)祝大家新年渐进步步高。

## 斐波那契实现数组相加

```java
public class Main {
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

​ 有两堆石子，有两个绝顶聪明的人在玩一个游戏，每次每个人可以从一堆石子中取任意数量但不少于1个的石子，或从两堆中同时取走相同数量的石子，最后一个取完石子的人获胜。

递归整数翻转

```java
public class Main {

    public static void main(String[] args) {
        System.out.println(reserve("abcd",3));
    }

    public static String reserve(String src, int end){
        if (end == 0) return ""+ src.charAt(0);
        return src.charAt(end)+reserve(src,end-1);
    }
}
```

## 整数的划分问题

对于正整数n=6，可以分划为：

6

5+1

4+2, 4+1+1

3+3, 3+2+1, 3+1+1+1

2+2+2, 2+2+1+1, 2+1+1+1+1

1+1+1+1+1+1+1

## 汉诺塔

```java
import java.util.Scanner;

public class Hanotower {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int num = input.nextInt();

        hanno(num, "A", "B", "C");
    }

    public static void hanno(int num, String from, String help, String to) {
        if (num == 1) {
            System.out.println("move " + num + "from" + from + "to" + to);
            return;
        }

        hanno(num - 1, from, to, help);
        System.out.println("move " + num + "from" + from + "to" + to);
        hanno(num - 1, help, from, to);
    }
}
```

# 2的幂表

| 2的幂 |      准确值       | 近似值 | x字节转换成MB、GB等 |
| :---: | :---------------: | :----: | :-----------------: |
|   7   |        128        |        |                     |
|   8   |        256        |        |                     |
|  10   |       1024        |  一千  |         1K          |
|  16   |      65 536       |        |         64K         |
|  20   |     1 048 576     | 一百万 |         1MB         |
|  30   |   1 073 741 824   |  十亿  |         1GB         |
|  32   |   4 294 967 296   |        |         4GB         |
|  40   | 1 099 511 627 776 | 一万亿 |         1TB         |

# 小白上楼梯（递归）

小白正在上楼梯，楼梯有n阶台阶，小白一次可以上一阶、两阶或者3阶，实现一个方法，计算小白有多少种走完楼梯的方法。

```java
public class UpStair {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int num = input.nextInt();
        int res = f(num);
        System.out.println(res);
    }

    public static int f(int num) {

        if (num <= 0) return 0;
        if (num == 1) return 1;
        if (num == 2) return 2;
        if (num == 3) return 4;

        return f(num - 1) + f(num - 2) + f(num - 3);

    }
}
```

# 旋转数组的最小数字（改造二分法）

​ 把一个属猪最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的一个旋转，输出旋转数组的最小元素。例如数组{3，4，5，1，2}为【1，2，3，4，5】的一个旋转，该数组的最小值为1

# 在有空字符串的有序字符串数组中查找

​ 有个排序后的字符串数组，其中散布着一些空字符串，编写一个方法，找出给定字符串（肯定不是空字符串）的索引。

```java
public class Solution02 {

    public static void main(String[] args) {
        String[] arr = {"a", "", "ac", "ad", "b", "", "ba"};
        int res = indexOf(arr, "abc");
        System.out.println(res);
    }

    private static int indexOf(String[] arr, String p) {
        int begin = 0;
        int end = arr.length - 1;
        while (begin <= end) {
            int indexOfMid = begin + ((end - begin) >> 1);
            while (arr[indexOfMid].equals("")) {
                indexOfMid++;
                if (indexOfMid > end) {
                    return -1;
                }
            }
            if (arr[indexOfMid].compareTo(p) > 0) {
                end = indexOfMid - 1;
            } else if (arr[indexOfMid].compareTo(p) < 0) {
                begin = indexOfMid + 1;
            } else {
                return indexOfMid;
            }
        }
        return -1;
    }
}
```

# 最长连续递增子序列（部分有序）

{1,9,2,5,7,3,4,6,8,0}中最长的递增子序列为{3,4,6,8}

dp算法

```java
public class Solution03 {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int num = Integer.parseInt(input.nextLine());
        int[] arr = new int[num];
        String[] res = input.nextLine().split(" ");
        for (int i = 0; i < res.length; i++) {
            arr[i] = Integer.parseInt(res[i]);
        }
        int[] dp = new int[num];

        for (int i = 0; i < arr.length; i++) {
            int max = 0;
            for (int j=i-1;j>=0;j--){
                if (arr[j]<=arr[i]){
                    int temp = dp[j];
                    max = Math.max(max,temp);
                }
            }
            dp[i]=max+1;
        }
        for (int i=0;i<num;i++){
            System.out.print(dp[i]+" ");

        }

    }
}
```

```java
public class Main {
    public static void main(String[] args) {

        //输入
        Scanner sr = new Scanner(System.in);
        int n = Integer.parseInt(sr.nextLine());
        int[] res = new int[n];
        String s[] = sr.nextLine().split(" ");
        for (int i = 0; i < n; i++)
            res[i] = Integer.parseInt(s[i]);


        int max = 0, count = 0, ss = 0, x = 0, y = 0;
        for (int i = 0; i < n - 1; i++) {
            y = i + 1;//判断是否递增，是的话count++;
            if (res[i + 1] > res[i]) {
                count++;
                if (count > max) {
                    max = count;
                    ss = x;
                }
            } else {
                count = 0;
                x = y;//不连续递增，则索引改变为下一个目标
            }
        }

        for (int i = ss; i <= ss + max; i++) {
            if (i == (ss + max)) {
                System.out.print(res[i]);
            } else {
                System.out.print(res[i] + " ");
            }
        }
    }

}
```

排序：

1.分治思想：快速排序、归并排序

2.小和、逆序对等问题求解

3.空间结构之法：堆排序、计数排序等

4.排序算法小节

分治法：

