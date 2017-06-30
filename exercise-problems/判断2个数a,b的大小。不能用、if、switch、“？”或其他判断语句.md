>通过符号位判断，由于int是32位，第32位是符号位，所以将两个数做差，将差值右移31位，正数的符号位为0，负数的符号位为1。

````
    public static void main(String[] args) {
        int a = 8;
        int b = 5;
        int[] c = {a, b};
        int d = a - b;
        d = d >> 31;
        d=d*-1;
        System.out.println(c[d]);
    }
````
