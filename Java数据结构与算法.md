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

