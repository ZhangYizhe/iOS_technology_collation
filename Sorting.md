## 排序

#### 快速排序

通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

```swift
class QuickSort {
    
    //特殊关键字标注 inout 将值类型的对象用引用的方式传递
    
    func sort(list _list: Array<Int>) -> Array<Int> { // 暴露出来的排序方法
        var list = _list
        quickSort(list: &list, low: 0, high: list.count - 1)
        return list
    }
    
    private func quickSort(list: inout Array<Int>, low: Int, high: Int) {
        if low < high {
            let mid = partition(list: &list, low: low, high: high) // 获得排序后基准数位置
            quickSort(list: &list, low: low, high: mid - 1) // 递归左半边
            quickSort(list: &list, low: mid + 1, high: high) // 递归右半边
        }
    }
    
    private func partition(list: inout Array<Int>, low _low: Int,high _high: Int) -> Int {
        var low = _low // 基准数 位置1
        var high = _high
        let temp = list[low] //基准数
        while low < high {
            while low < high && temp < list[high] { // 从右向左 查找小于基准数的 位置2
                high -= 1
            }
            list[low] = list[high] // 将小于基准数的数字填入基准数 位置1
            while low < high && temp > list[low] { // 从左向右 查找大于基准数的 位置3
                low += 1
            }
            list[high] = list[low] // 将大于基准数的数字填入前面小于基准数的数字的位置 位置2
        }
        list[low] = temp // 将基准数填入 位置3
        return low // 基准数位置返回
    }
}

var data = [5,4,3,1,6,2,7]
print(QuickSort().sort(list: data))
```

#### 冒泡排序

重复地走访过要排序的数列，一次比较两个元素，如果它们的顺序错误就把它们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成

```swift
var data = [5,4,3,1,6,2,0]
var sortflag = true
while sortflag {
    sortflag = false
    for i in 0..<data.count-1 {
        if data[i] > data[i+1] {
            let temp = data[i]
            data[i] = data[i+1]
            data[i+1] = temp
            sortflag = true
        }
    }
}
print(data)
```

