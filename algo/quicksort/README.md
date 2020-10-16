# QuickSort

The following is an algorithm which implements quicksort with random pivot selection.

```python
#!/usr/bin/python3
import random

'''
This funciton implements QuickSort (ascendingly)
arr: an array to be sorted
start: starting index of sorting
end: ending index of sorting
'''
def quicksort(arr, start, end):
    if(start<end):
        # pivotindex is the index where the pivot lies in the array
        # the partition function returns pivoitindex and separately sorts the array around the pivot
        pivotindex=partition_r(arr,start, end)
        quicksort(arr, start, pivotindex-1)
        quicksort(arr, pivotindex+1, end)
    
'''
This funciton randomly generates a pivot to avoid worse case O(n^2), and 
                calls a function to sort the array around the pivot
'''
def partition_r(arr, start, end):
    # randomly select an index as pivot index
    randpivotindex=random.randrange(start, end)
    
    # since the partition funciton assigns the last element as the pivot, swap the randomly selected element and the last element
    arr[randpivotindex], arr[end] = arr[end], arr[randpivotindex]
    return partition(arr, start, end) 
    
'''
This funciton takes last element as pivot,
                places all smaller (smaller than pivot) to left of pivot and all greater elements to right of pivot, and 
                places the pivot at its correct position in sorted array and returns that pivot index
'''
def partition(arr, start, end):
    # assign the last element as the pivot
    pivot=arr[end]
    
    # the largest index of elements which are smaller than the pivot
    # -1 for no element is smaller than the pivot
    smallindex=start-1
    
    # move elements which are smaller than pivot to the left of it
    for i in range(start, end):
        if(arr[i]<pivot):
            smallindex+=1
            arr[smallindex], arr[i] = arr[i], arr[smallindex]
            
    # places the pivot at its correct position in sorted array
    arr[smallindex+1], arr[end] = arr[end], arr[smallindex+1]
    
    return smallindex+1
    
'''
Driver code
'''
if __name__ == "__main__":
    array = [10, 7, 8, 9, 1, 5]
    quicksort(array, 0, len(array) - 1)
    print(array)
```
