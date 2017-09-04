# 快速排序算法

快速排序算法是排序算法中应用范围最广的一种算法，java中的默认Arrays.sort\(\) 即采用了排序算法作为其实现。

排序算法在面试过程中也经常直接或间接被考察到。他的实现涉及到了很多重要而细小的知识点，体现了很多数据结构的思想。所以建议经常联系快速排序算法，就好像练习毛笔字的人经常练习“永”字一样，经常联系快速排序算法，也可以通过一道题目练习到很多的知识点。

快速排序的一次实现：

```
public void quickSort(int[] array){
    if(array == null){
        return;
    }
    quickSort(array,0,array.length -1);
}
```

在这里，quickSort方法内部调用了另外一个quickSort方法，他们的输入参数并不一样，这叫做Method Overloading。

```
quickSort(int[] array,int left, int right){

}
```



