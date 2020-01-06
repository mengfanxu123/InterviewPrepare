# sort

### Bubble Sort

```java
public static void sort(int arr[]){
    for( int i = 0 ; i < arr.length - 1 ; i++ ){
        for(int j = 0;j < arr.length - 1 - i ; j++){
            int temp = 0;
            if(arr[j] < arr[j + 1]){
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
// time complexity O(n^2)
```

### select sort

```java
public void selectSort(int[] nums){
    for (int i = 0; i < nums.length; i++){
    int min = i;
      for (int j = i + 1; j < nums.length; j++){
        if(nums[j] < nums[i]){
          min = j;
        }
      }
      int temp = arr[i];
      arr[i] = arr[min];
      arr[min] = temp;
    }
}
```

### Insert Sort

```java
public static void sort(int[] arr){
    int n = arr.length;
    for (int i = 1; i < n; ++i){
        int value = arr[i];
        int j = 0; // insert position
        for (j = i - 1; j >= 0; j--){
            if(arr[j] > value){
                arr[j + 1] = arr[j];
            } else {
                break;
            }
        }
        arr[j + 1] = value;
    }
}

time best O(n) worst O(n ^ 2)
```

### Merge Sort

```java
 public static void sort(int[] arr) {
        int[] tempArr = new int[arr.length];
        sort(arr， tempArr， 0， arr.length-1);
    }

    /**
     * 归并排序
     * @param arr 排序数组
     * @param tempArr 临时存储数组
     * @param startIndex 排序起始位置
     * @param endIndex 排序终止位置
     */
    private static void sort(int[] arr，int[] tempArr，int startIndex，int endIndex){
        if(endIndex <= startIndex){
            return;
        }
        //中部下标
        int middleIndex = startIndex + (endIndex - startIndex) / 2;

        //分解
        sort(arr，tempArr，startIndex，middleIndex);
        sort(arr，tempArr，middleIndex + 1，endIndex);

        //归并
        merge(arr，tempArr，startIndex，middleIndex，endIndex);
    }

    /**
     * 归并
     * @param arr 排序数组
     * @param tempArr 临时存储数组
     * @param startIndex 归并起始位置
     * @param middleIndex 归并中间位置
     * @param endIndex 归并终止位置
     */
    private static void merge(int[] arr， int[] tempArr， int startIndex， int middleIndex， int endIndex) {
        //复制要合并的数据
        for (int s = startIndex; s <= endIndex; s++) {
            tempArr[s] = arr[s];
        }

        int left = startIndex;//左边首位下标
        int right = middleIndex + 1;//右边首位下标
        for (int k = startIndex; k <= endIndex; k++) {
            if(left > middleIndex){
                //如果左边的首位下标大于中部下标，证明左边的数据已经排完了。
                arr[k] = tempArr[right++];
            } else if (right > endIndex){
                //如果右边的首位下标大于了数组长度，证明右边的数据已经排完了。
                arr[k] = tempArr[left++];
            } else if (tempArr[right] < tempArr[left]){
                arr[k] = tempArr[right++];//将右边的首位排入，然后右边的下标指针+1。
            } else {
                arr[k] = tempArr[left++];//将左边的首位排入，然后左边的下标指针+1。
            }
        }
    }
    
    //time O(nlogn)
    //space O(n)
```

### Quick Sort

快速排序的核心思想也是分治法，分而治之。它的实现方式是每次从序列中选出一个基准值，其他数依次和基准值做比较，比基准值大的放右边，比基准值小的放左边，然后再对左边和右边的两组数分别选出一个基准值，进行同样的比较移动，重复步骤，直到最后都变成单个元素，整个数组就成了有序的序列。

```java
public static void sort(int[] arr) {
    sort(arr， 0， arr.length - 1);
}

private static void sort(int[] arr， int startIndex， int endIndex) {
    if (endIndex <= startIndex) {
        return;
    }
    //切分
    int pivotIndex = partitionV2(arr， startIndex， endIndex);
    sort(arr， startIndex， pivotIndex-1);
    sort(arr， pivotIndex+1， endIndex);
}

private static int partition(int[] arr， int startIndex， int endIndex) {
    int pivot = arr[startIndex];//取基准值
    int mark = startIndex;//Mark初始化为起始下标

    for(int i=startIndex+1; i<=endIndex; i++){
        if(arr[i]<pivot){
            //小于基准值 则mark+1，并交换位置。
            mark ++;
            int p = arr[mark];
            arr[mark] = arr[i];
            arr[i] = p;
        }
    }
    //基准值与mark对应元素调换位置
    arr[startIndex] = arr[mark];
    arr[mark] = pivot;
    return mark;
}

```

