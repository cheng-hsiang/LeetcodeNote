# LeetcodeNote


### 


###  15. 3Sum
![image](https://user-images.githubusercontent.com/37887893/228558829-d23f4a19-12cd-44cd-ad79-db4cf7234474.png)

3Sum指的是在一個數組中，找出三個數的和為0

先對傳入的數組進行排序，從小到大排列。

遍歷每個元素，作為第一個數，並從這個數的下一個位置開始，分別取左右兩個指針，分別表示第二個數和第三個數。

内部使用了一個while循環，當左右指針交錯時則退出。

在while內，先求出三個指針所指的數的和(sum)，如果是0就加入到結果數組res中，大於0小於0做加減，盡可能接近0

當左右指针移到下一个位置时，已經比較過則跳過


```
var threeSum = function(nums) {
    if(typeof nums === 'undefined' || nums.length < 3){
        return [];
    }
    let res = []
    const sortedNums = [...nums].sort((a, b) => a - b);
    for(let i=0; i<sortedNums.length - 2; i++){
        if(sortedNums[i] > 0) { break; } // no result possible if this is positive
        if (i > 0 && sortedNums[i] === sortedNums[i - 1]) { continue; } // skip duplicate values
        let left = i + 1;
        let right = sortedNums.length - 1;
        while(left < right){
            let sum = sortedNums[i] + sortedNums[left] + sortedNums[right];
            if(sum === 0){
                res.push([sortedNums[i], sortedNums[left], sortedNums[right]]);
                while (left < right && sortedNums[left] === sortedNums[left+1]) left++; // skip duplicate values
                while (left < right && sortedNums[right] === sortedNums[right-1]) right--; // skip duplicate values
                left++;
                right--;
            } else if(sum < 0){
                left++;
            } else {
                right--;
            }
        }
    }
    return res;
};

```
