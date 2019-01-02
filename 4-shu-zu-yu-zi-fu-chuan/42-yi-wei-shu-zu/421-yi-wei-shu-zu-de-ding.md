```
数据类型[] 数组名;//声明以为数组
数组名 = new 数据类型[个数];//分配内存给数据
```

数组类Arrays的常用方法

| 方法 | 说明 |
| :--- | :--- |
| public static int binarySearch\(X\[\] a,X key\) | X是任意数据类型。返回key在升序数组a中首次出现的下标，若a中不包含key，则返回负值 |
| public static void sort\(X\[\] a\) | X是任意数据类型。对数组a升序排序后仍放在a中 |
| public static void sort\(X\[\] a,int fromIndex,int toIndex\) | 对任意类型的数组a中从fromIndex到toIndex-1的元素进行升序排序，其结果仍放在a数组中 |
| public static X\[\] copyOf\(X\[\] original,int newLength\) | 截取任意类型数组original中长度为newLength的数组元素拷贝给调用数组 |
| public static boolean equals\(X\[\] a,X\[\] a2\) | 判断同类型的两个数组a和a2中对应元素值是否相等。若相等则返回true，否则返回false |



