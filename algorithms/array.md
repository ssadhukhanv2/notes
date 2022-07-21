## **Arrays**

* [What are Arrays?](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2) 
    * **Arrays** are used to store multiple items in one place and these item are typically of the same datatype. 
    * **Difference with Linked List, Self Balancing BST or Hash** Arrays store the items in contigous memory location. With Linked List, Self Balancing BST or Hash items are not stored in contigous memory location.
    
            int[] arr=new int[]{1,2,3,4,5,6,7,8};
        This creates an array of 8 elements. So the size of the array is 8. The array is indexed from 0 to 7. So arr[0]=1, arr[1]=2, arr[2]=3 and so on

    **Algorithms:**
    * **``Find index of Highest Element in an Array``**
    * **``How will you Reverse an Array``**
    * **``Check if an array is sorted``**
    * **``Find the Index of the Second Highest Element in an Array``**
    * **``How will you remove duplicate elements from  sorted Array``**
    * **``how will you move the zeros to the end of the array``**

* [Find the Index of Second Highest Element in an Array using O(n) complexity](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2) 
  * **Second Highest Element in an Array:** If you consider your array as a stream of data and if you traverse this stream from left to right then you can keep track of the highest and second highest element till this point.

        public static int getIndexOfSecondHighestElement(int[] arr) {
            var n = arr.length;
            int highest = n - 1;
            int secondHighest = -1;
            for (int i = 0; i < arr.length - 1; i++) {
                if (arr[i] > arr[highest]) {
                    secondHighest = highest;
                    highest = i;
                } else if (arr[i] != arr[highest]) {
                    if (secondHighest == -1 || arr[i] > arr[secondHighest]) {
                        secondHighest = i;
                    }
                }
            }
            return secondHighest;
        }

        int[] arrUnSorted=new int[]{3, 8, 4, 5, 7, 1};
        int resultSorted = getIndexOfSecondHighestElement(arrUnSorted);
        Assertions.assertEquals(4, arrUnSorted);

    

* [Check if an array is sorted](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2)

        public static boolean isArraySorted(int[] arr) {
            var n = arr.length;
            for (int i = 1; i < n; i++) {
                if (arr[i - 1] > arr[i])
                    return false;
            }
            return true;
        }


* [How will you Reverse an Array](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2)
        
        public static void reverse(int[] arr) {
            var left = 0;
            var right = arr.length - 1;
            while (left < right) {
                swap(arr, left, right);
                left++;
                right--;
            }
        }
        
        int[] arrUnSorted=new int[]{3, 8, 4, 5, 7, 1};
        ArrayUtil.reverse(arrUnSorted);
        Assertions.assertThat(arrUnSorted)
                .containsExactly(1, 7, 5, 4, 8, 3);

* [How will you remove duplicate elements from  sorted Array using O(n) complexity and O(1) auxilary space](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2) We initialize the count as 1, incase the array is not empty. This indicates that there will be atleast one distinct element if the array is not empty. We then start at 1 and compare every element with the last element that we included in our result. If the elements are not same, we copy the element to the corresponding position of i & increment the count. The final count is te number of distict element in the array and the indexes 0 to count-1 having the distinct elements.
* INPUT: &nbsp;&nbsp;&nbsp;&nbsp;{10, 5, 0, 0, 8, 0, 9, 0}
* OUTPUT: &nbsp;{10, 5, 8, 9, 0, 0, 0, 0}


        public static int removeDuplicatesFromSortedArray(int[] arr) {
            if (arr.length < 1) {
                return -1;
            }
            var n = arr.length;
            var count = 1;
            for (var i = 1; i < n; i++) {
                if (arr[i] != arr[count - 1]) {
                    arr[count] = arr[i];
                    count++;
                }
            }
            return count;
        }
        var arr = new int[]{1, 1, 1, 1, 3, 3, 4, 4, 4, 4, 4, 5, 7, 7, 7, 8};
        int result = ArrayUtil.removeDuplicatesFromSortedArray(arr);
        Assertions.assertEquals(6, result);
        org.assertj.core.api.Assertions.assertThat(arr)
                .containsExactly(1, 3, 4, 5, 7, 8, 4, 4, 4, 4, 4, 5, 7, 7, 7, 8);


* [In an array having zero and non zero element, how will you move the zeros to the end of the array, while preserving existing order of nonzero elements](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=154&tab=2)
    * INPUT: &nbsp;&nbsp;&nbsp;&nbsp;{10, 5, 0, 0, 8, 0, 9, 0}
    * OUTPUT: &nbsp;{10, 5, 8, 9, 0, 0, 0, 0}
  * **``Naive Solution:``** Traverse the elements from left side and as soon as we find a zero we replace it with the first non zero element to it's right. Time Complexity: **``O(n^2)``**

        public static void moveZerosToTheEnd(int[] arr) {
            int n = arr.length;
            for (int i = 0; i < n; i++) {
                if (arr[i] == 0) {
                    for (int j = i + 1; j < n; j++) {
                        if (arr[j] != 0) {
                            swap(arr, i, j);
                            break;
                        }
                    }
                }
            }
        }
        var arr = new int[]{10, 5, 0, 0, 8, 0, 9, 0};
            ArrayUtil.moveZerosToTheEnd(arr);
            org.assertj.core.api.Assertions.assertThat(arr)
                    .containsExactly(10, 5, 8, 9, 0, 0, 0, 0);


  * **``Efficient Solution:``**: Traverse the elements of the array and keep count of non-zero elements traversed till now. This count is always equal to the first index of zero.  So if non zero element is encountered, simply swap it with the element at count. Time Complexity: **``O(n)``**

        public static void moveZerosToTheEnd(int[] arr) {
            int n = arr.length;
            int count = 0;
            for (int i = 0; i < n; i++) {
                if (arr[i] != 0) {
                    swap(arr, i, count);
                    count++;
                }
            }
        }
