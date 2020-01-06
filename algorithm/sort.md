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

