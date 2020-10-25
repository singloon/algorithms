# Algorithms

## Bubble sort (Сортировка пузырьком)
Bubble sort compares each pair of elements in a list and swaps them if they are out of order until the list is sorted. Like insertion sort, bubble sort is a comparison algorithm and runs in O(n²) time, making it an inefficient algorithm for larger lists.

### Visual
![Bubble sorting](bubbleSort/bubbleSort.gif)

### Code:
```javascript
function bubbleSort(arr) {
    var done = false;
  
    while(!done){
      done = true;
        for (var i = 0; i < arr.length - 1; i++) {
            if (arr[i] > arr[i+1]) {
                var temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
                done = false;
            }
        }
    }
    return arr;
}

bubbleSort([2, 6, 1, 9, 3, 8, 5, 4, 7]);
```

## Selection sort (Сортировка выбором)
A sort algorithm that repeatedly searches remaining items to find the least one and moves it to its final location. The run time is O(n²), where n is the number of elements. The number of swaps is O(n).

### Visual
![Selection sorting](selectionSort/selectionSort.gif)

### Code:
```javascript
function selectionSort(arr){
    for (let i = 0; i < arr.length; i++) {
        let min = i;
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[min] > arr[j]) {
                min = j;
            }
        }
        if (min !== i) {
            let tmp = arr[i];
            arr[i] = arr[min];
            arr[min] = tmp;
        }
    }
    return arr;
}

selectionSort([1, 5, 6, 2, 3, 8, 4, 7, 9]);
```

## Insertion sort (Сортировка вставками)
Insertion sort is a simple sorting algorithm that works the way we sort playing cards in our hands. This sort is based on the idea that one element from the input elements is consumed in each iteration to find its correct position i.e, the position to which it belongs in a sorted array. Since is the first element has no other element to be compared with, it remains at its position. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort.

### Visual
![Insertion sorting](insertionSort/insertionSort.gif)

### Code:
```javascript
function insertionSort(arr){
  for (var i = 1; i < arr.length; i++){
    if (arr[i] < arr[0]){
      //move current element to the first position
      arr.unshift(arr.splice(i,1)[0]);
    }else if (arr[i] > arr[i-1]){
      //leave current element where it is
      continue;
    }else{
      //find where element should go
      for (var j = 1; j < i; j++){
        if (arr[i] > arr[j-1] && arr[i] < arr[j]){
          //move element
          arr.splice(j,0,arr.splice(i,1)[0]);
        }
      }
    }
  }
  return arr;
}

insertionSort([3, 0, 2, 5, 6, 4, 1]);
```

## Linear search (Линейный поиск)
In this algorithm, you can stop when the item is found and then there is no need to look further. In the best case, you could get lucky and the item you are looking at maybe at the first position in the array! But in the worst case, you would have to look at each and every item before you find the item at the last place or before you realize that the item is not in the array. The complexity therefore of the linear search is: O(n). If the element to be searched presides on the the first memory block then the complexity would be: O(1).

### Visual
![Linear search](linearSearch/linearSearch.gif)

### Code:
```javascript
function linearSearch(arr, item) {
  // Go through all the elements of arr to look for item.
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] === item) { // Found it!
      return i;
    }
  }
  // Item not found in the array.
  return null;
}

linearSearch([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20], 13);
```

## Binary search (Бинарный поиск)
Binary search is an algorithm used to find a particular item in a **sorted list**. It’s essential for the list to be sorted beforehand or the algorithm won’t be applicable. If you’ve ever dealt with binary search trees, this concept of this algorithm is similar. In each step, the algorithm compares the input element x with the value of the middle element in array. If the values match, return the index of middle. Otherwise, if x is less than the middle element, then the algorithm recurs for left side of middle element, else recurs for right side of middle element.

### Visual
![Binary search](binarySearch/binarySearch.gif)

### Code:
```javascript
function binarySearch(arr, target) {
    let first = 0;
    let last = arr.length - 1;
    let position = -1;
    let found = false;
    let middle;

    while (found === false && first <= last) {
        middle = Math.floor((first + last) / 2);
        if (arr[middle] == target) {
            found = true;
            position = middle;
        }else if (arr[middle] > target){
            last = middle - 1;
        }else{
            first = middle + 1;
        }
    }
    return position;
}

binarySearch([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20], 13);
```

## Quicksort (Быстрая сортировка)
Quick sort is an efficient divide and conquer sorting algorithm. Average case time complexity of Quick Sort is O(nlog(n)) with worst case time complexity being O(n^2).

The steps involved in Quick Sort are:

- Choose an element to serve as a pivot, in this case, the last element of the array is the pivot.
- Partitioning: Sort the array in such a manner that all elements less than the pivot are to the left, and all elements greater than the pivot are to the right.
- Call Quicksort recursively, taking into account the previous pivot to properly subdivide the left and right arrays. (A more detailed - - explanation can be found in the comments below)

### Visual
![Quicksort](quickSort/quickSort2.gif)
![Quicksort](quickSort/quickSort.gif)

### Code:
```javascript
function swap(items, leftIndex, rightIndex){
    var temp = items[leftIndex];
    items[leftIndex] = items[rightIndex];
    items[rightIndex] = temp;
}
function partition(items, left, right) {
    var pivot   = items[Math.floor((right + left) / 2)], //middle element
        i       = left, //left pointer
        j       = right; //right pointer
    while (i <= j) {
        while (items[i] < pivot) {
            i++;
        }
        while (items[j] > pivot) {
            j--;
        }
        if (i <= j) {
            swap(items, i, j); //sawpping two elements
            i++;
            j--;
        }
    }
    return i;
}

function quickSort(items, left, right) {
    var index;
    if (items.length > 1) {
        index = partition(items, left, right); //index returned from partition
        if (left < index - 1) { //more elements on the left side of the pivot
            quickSort(items, left, index - 1);
        }
        if (index < right) { //more elements on the right side of the pivot
            quickSort(items, index, right);
        }
    }
    return items;
}

var items = [5,3,7,6,2,9];
quickSort(items, 0, items.length - 1);
```

## Counting sort (Сортировка подсчётом)
Counting sort is a sorting algorithm that sorts the elements of an array by counting the number of occurrences of each unique element in the array. It works on a limited set of elements. The count is stored in an auxiliary array and the sorting is done by mapping the count as an index of the auxiliary array. It runs in O(n + k) where n is the number of elements in the input array and k is the maximum key.

### Code:
```javascript
function countingSort(arr, max) {
    const count = new Array(max + 1);
    for (let i = 0; i < max + 1; ++i) count[i] = 0;

    for (let i = 0; i < arr.length; ++i) count[arr[i]] += 1;

    let total = 0;
    for (let i = 0; i < count.length; ++i) {
        const prevTotal = total;
        total += count[i];
        count[i] = prevTotal;
    }

    const output = arr.slice();
    for (let i = 0; i < arr.length; ++i) {
        output[count[arr[i]]] = arr[i];
        count[arr[i]] += 1;
    }
    return output;
}

countingSort([1, 2, 3, 2, 7, 9, 1, 0], 9);
```

## Merge sort (Сортировка слиянием)

## Heapsort (Пирамидальная сортировка)
