# 十大经典排序算法

## 选择排序

```js
/**
 * 选择排序 O(n^2)
 * 核心算法是在未排序数据中找到最小值，存放到排序序列开始位置
 * @param { Array } arr 
 * @returns { Array } 
 */
function selectSort(arr) {
	const length = arr.length;
	let minIndex;

	for (let i=0; i<length; i++) {
			minIndex = i;
			for (let j=i+1; j<length; j++) {
				if (arr[j] < arr[minIndex]) {
					minIndex = j;
				}
			}

			swap(arr, i, minIndex)
	}

	return arr;
}
```

## 插入排序

```js
/**
 * 插入排序 O(n^2)
 * 核心实现：提前终止内层循环，使用赋值，避免 swap 交换，当元素是有序时，插入算法将会是一个 O(n) 级别的
 * 内存循环元素如果比当前的元素 e 大，元素后移
 * 内层循环元素如果比当前的元素 e 小，直接 Break 跳出循环，将 e 插入适当位置
 * @param { Array } arr 
 * @returns { Array }
 */
function insertSort(arr) {
	const length = arr.length;

	for (let i=1; i<length; i++) {
		let j;
		let e=arr[i];

		// for (j=i; j>0; j--) {
		// 	if (arr[j-1] > e) {
		// 		arr[j] = arr[j-1];
		// 	} else {
		// 		break;
		// 	}
		// }

		// 上面注释部份的一种精简写法
		for (j=i; j>0 && arr[j-1] > e; j--) {
			arr[j] = arr[j-1];
		}

		arr[j] = e;
	}

	return arr;
}
```

## 快速排序

```js
function quickSort(arr) {
	_quickSort(arr, 0, arr.length-1);
}

function _quickSort(arr, l, r) {
	if (l >= r) return;

	const p = _partition(arr, l, r);
	_quickSort(arr, l, p-1);
	_quickSort(arr, p+1, r);
}

function _partition(arr, l, r) {
	const v = arr[l];
	let j = l;

	for (let i=l+1; i<=r; i++) {
		if (arr[i] < v) {
			swap(arr, j+1, i);
			j++;
		}
	}

	swap(arr, l, j);
	return j;
};
```

## 归并排序

归并排序是分而治之算法的经典应用，将数据一分为二，进行归并操作，时间复杂度为 O(nlogn)。

```js
/**
 * 归并排序，自上而下方式
 * @param { Array } arr 
 */
function mergeSort(arr) {
  const len = arr.length;

  if (len <=1 ) return arr;

  const mid = Math.floor(len/2);
  const leftArr = arr.slice(0, mid);
  const rightArr = arr.slice(mid);

  return merge(mergeSort(leftArr), mergeSort(rightArr));
}

function merge(leftArr, rightArr) {
  const res = [];

  while(leftArr.length && rightArr.length) {
    leftArr[0] < rightArr[0] ? res.push(leftArr.shift()) : res.push(rightArr.shift());
  }

  while(leftArr.length) {
    res.push(leftArr.shift());
  }

  while(rightArr.length) {
    res.push(rightArr.shift());
  }

  return res;
}
const arr = [11,5,2,7,4,9,10];
console.log(mergeSort(arr))

const a=[2,5,11], b=[4,7,9,10];
console.log(merge(mergeSort(a), mergeSort(b)));
```

## 参考

* [github.com/hustcc/JS-Sorting-Algorithm](https://github.com/hustcc/JS-Sorting-Algorithm)