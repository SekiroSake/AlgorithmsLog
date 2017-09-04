# 快速排序算法

快速排序算法是排序算法中应用范围最广的一种算法，java中的默认Arrays.sort\(\) 即采用了排序算法作为其实现。

排序算法在面试过程中也经常直接或间接被考察到。他的实现涉及到了很多重要而细小的知识点，体现了很多数据结构的思想。所以建议经常练习快速排序算法，就好像练习毛笔字的人经常练习“永”字一样，经常练习快速排序算法，可以通过这一道题目练习到很多的知识点。

快速排序实现的开始：

```
public void quickSort(int[] array){
    if(array == null){
        return;
    }
    quickSort(array,0,array.length -1);
}
```

在这里，quickSort方法内部调用了另外一个quickSort方法，他们的输入参数并不一样，这叫做Method Overloading，同一个方法名，不同的实现方式。

```
quickSort(int[] array,int left, int right){
    if(left >= right){
        return;
    }
    int pivotIndex = partition(array,left, right);
    quickSort(array,left, pivotIndex - 1);
    quickSort(array,pivotIndex + 1, right);

}
```

Corner case分析：

* 为什么left&gt;=right的时候return（而不是left &gt; right 甚至left &gt; right - 1）?

这里需要考虑的就是快速排序的极限情况，只剩下左右两个点时，要不要排序？答案是要排序（所以left &gt; right -1排除）,左右点是同一个点要不要排序？答案是不需要，这时候我们的一个子排序已经走到尽头，return即可。left &gt; right 需不需要排序？更不需要排序。所以边界条件是left &gt;= right；

* 为什么递归函数的传入值不包含pivotIndex本身？

pivotIndex是一次排序的返回值，在这个点，左边的数一定小于他，右边的数一定大于他，所以这个点不能带入下一次递归。

```
partition（int[] array, int left, int right）{
    int pivotPosition = randomPivot(left, right);
    int leftBound = left;
    int rightBound = right - 1;
    int pivotValue = array[pivotPosition];
    swap(array,pivotPosition,right);
    while(leftBound < = rightBound){
        if(array[leftBound] < pivotValue){
            leftBound++;
        }else if (array[rightBound] >= pivotValue){
            rightBound--;
        }else{
            swap(array,leftBound++,rightBound--);
        }
    }
    swap(array,leftBound,right);
}
```

Corner Case 分析：

* 为什么是leftBound &lt;= rightBound？

毋庸置疑的是leftBound &lt; rightBound的时候，肯定要进行排序。问题是leftBound等于rightBound的时候呢？答案是依然需要，因为跟这些移动的pivot作比较的是那个pivot值，这个值在开始排序前被swap到了array 的末尾。及时leftBound和rightBound是同一个点了，我们依然要把这个点跟pivot的值进行比较。

* 为什么最后的swap是leftBound和right？

紧跟着上面，当左右是同一个点了，这个时候假设左边依然比pivotValue小，（假设3xxx5,左右点都在3，pivot是5）leftBound +1，循环结束。在leftBound（+1后）左边的所有数都比他小，而这里的rightBound实际上是3 ，我们只有把当前的leftBound跟array末尾的pivot进行swap，才能保证3还是在5的左边。最极限的情况（35），leftBound + 1之后就移动到了5，最后5和5本身swap，依然保证了3在5的前面。

```
private int getRandomPivot(int left, int right){
        return left + (int)Math.random()*(right - left + 1);
    }


private void swap(int[] array, int left, int right) {
        int temp = array[right];
        array[right] = array[left];
        array[left] = temp;
    }
```



