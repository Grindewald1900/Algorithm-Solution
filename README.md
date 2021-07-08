<!-- PROJECT LOGO -->

<p align="center">
  <a href="https://github.com/Grindewald1900/Notebook">
    <img src="https://assets.algoexpert.io/g1ec323b14b-prod/dist/social-logo.png" width="720" height="340">
  </a>
</p>
<h1 align="center">Solution to AlgoExpert</h1>
<h3 align="center">Grindewald1900 </h3>

<p align="left">
    <a href="" alt="Contributors">
        <img src="https://visitor-badge.glitch.me/badge?page_id=Grindewald1900.Leetcode-solution" /></a>
    <a href="https://github.com/Grindewald1900/Leetcode-solution/graphs/contributors" alt="Contributors">
        <img src="https://img.shields.io/github/contributors/Grindewald1900/Grindewald1900" /></a>
    <a href="https://github.com/Grindewald1900/Grindewald1900/pulse" alt="Activity">
        <img src="https://img.shields.io/github/commit-activity/m/Grindewald1900/Leetcode-solution" /></a>
    <a href="https://circleci.com/gh/Grindewald1900/Leetcode-solution/tree/master">
        <img src="https://img.shields.io/circleci/project/github/Grindewald1900/Leetcode-solution/master" alt="build status"></a>
    <a href="https://github.com/Grindewald1900/Notebook/blob/master/LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green"
            /></a> 
    <a href="https://www.linkedin.com/in/yee-ren-19940924/">
        <img src="https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555"
            /></a>
</p>

<!-- TABLE OF CONTENTS -->
### Table of Contents
*   [1. Array](#Part1)
*   [2. Binary Search Trees](#Part2)
*   [3. Binary Trees](#Part3)
*   [4. Dynamic Programming](#Part4)
*   [5. Famouse Algorithms](#Part5)
*   [6. Graph](#Part6)
*   [7. Greedy Algorithms](#Part7)
*   [8. Heaps](#Part8)
*   [9. Linked List](#Part9)
*   [10. Recursion](#Part10)
*   [11. Searching](#Part11)
*   [12. Sorting](#Part12)
*   [13. Stack](#Part13)
*   [12. String](#Part14)
*   [12. Tires](#Part15)


<a name = "Part1"></a>
### Array
#### 1.Two Number Sum
**Solution 1**
```Kotlin
fun twoNumberSum(array: MutableList<Int>, targetSum: Int): List<Int> {
    // Write your code here.
    for(a in array){
        if((targetSum - a) in array && array.indexOf(a) != array.indexOf(targetSum - a)){
            return listOf(a, targetSum - a)
        }
    }
    return listOf<Int>()
}
```

**Solution 2**
```Kotlin
fun twoNumberSum(array: MutableList<Int>, targetSum: Int): List<Int> {
    // Write your code here.
    array.sort()
    var left = 0
    var right = array.size - 1
    while (left < right){
        if(array[left] + array[right] > targetSum) 
            right--
        if (array[left] + array[right] < targetSum) 
            left++
        if (array[left] + array[right] == targetSum)
            return listOf<Int>(array[left], array[right])
    }
    return listOf<Int>()
}
```

#### 2.Validate Subsequence
**Solution 1**
```Kotlin
//O(n) time and O(n) space
fun isValidSubsequence(array: List<Int>, sequence: List<Int>): Boolean {
    var mutableArray = array.toMutableList()
    sequence.forEach {
        if(mutableArray.contains(it))
            mutableArray = mutableArray.subList(mutableArray.indexOf(it) + 1, mutableArray.size)
        else
            return false
    }
    return true
}
```


**Solution 2**
```Kotlin
// O(n) time and O(1) space
fun isValidSubsequence(array: List<Int>, sequence: List<Int>): Boolean {
    var arrayIndex = 0
    var seqIndex = 0
    while (arrayIndex < array.size && seqIndex < sequence.size){
        if(array[arrayIndex] == sequence[seqIndex]) seqIndex++
        arrayIndex++ 
    }
    return seqIndex == sequence.size
}
```


#### 3.Sorted Squared Array
**Solution 1**
```Kotlin
// O(nlogn) time and O(n) space
fun sortedSquaredArray(array: List<Int>): List<Int> {
    // Write your code here.
    val resultList = mutableListOf<Int>()
    array.forEach {
        resultList.add(it * it)
    }
    resultList.sort()
    return resultList
}
```


**Solution 2**
```Kotlin
// O(n) time and O(n) space
fun sortedSquaredArray(array: List<Int>): List<Int> {
    // Write your code here.
    val resultList = ArrayDeque<Int>()
    var leftIndex = 0
    var rightIndex = array.size - 1
    while (leftIndex <= rightIndex){
        if(abs(array[leftIndex]) <= abs(array[rightIndex])){
            resultList.push(array[rightIndex] * array[rightIndex])
            rightIndex --
        }else{
            resultList.push(array[leftIndex] * array[leftIndex])
            leftIndex ++
        }
    }
    return resultList.toMutableList()
}
```

#### 4.Tournament Winner
**Solution 1**
```Kotlin
// O(n) time and O(n) space
fun tournamentWinner(competitions: List<List<String>>, results: List<Int>): String {
    // Write your code here.
    val competiterList = hashMapOf<String, Int>()
    var maxValue = 0
    var champion = ""
    for (i in competitions.indices){
        val winner = competitions[i][1 - results[i]]
        if (!competiterList.containsKey(winner)){
            competiterList[winner] = 1
        }else{
            competiterList[winner] =  competiterList[winner]!! + 1
        }
    }
    competiterList.forEach{
        if(it.value > maxValue){
            maxValue = it.value
            champion = it.key
        }
    }
    return champion
}
```

#### 5.Non-Constructible Change
**Solution 1**
```Kotlin
// O(nlogn) time | O(1) space
fun nonConstructibleChange(coins: MutableList<Int>): Int {
    // Write your code here.
    coins.sort()
    var currentChange = 0
    coins.forEach {
        if (it > currentChange + 1)
            return currentChange + 1
        currentChange += it
    }
    return currentChange + 1
}
```


#### 6.Three Number Sum
**Solution 1**
```Kotlin
// O(n^2) time | O(n) space
fun threeNumberSum(array: MutableList<Int>, targetSum: Int): List<List<Int>> {
    // Write your code here
    val result: MutableList<MutableList<Int>> = mutableListOf()
    array.sort()
    array.forEach(fun(item: Int) {
        val subArray = array.toMutableList()
        subArray.remove(item)
        val twoSumArray = twoNumberSum(subArray, targetSum - item)
        if (twoSumArray.size > 0) {
            twoSumArray.forEach {
                if (item < it[0]){
                    val triplet = mutableListOf(item)
                    triplet.addAll(it)
                    result.add(triplet)
                }
            }
        }
    })
    return result
}

fun twoNumberSum(subArray: MutableList<Int>, sum: Int): MutableList<List<Int>>{
    val result: MutableList<List<Int>> = mutableListOf()
    subArray.forEach {
        if(subArray.contains(sum - it)){
           if (subArray.indexOf(sum - it) != subArray.indexOf(it)) {
               if(it <= sum/2){
                   result.add(listOf(it, sum - it))
               }
           }
        }
    }
    return result
}
```


#### 7.Smallest Difference
**Solution 1**
```Kotlin
// O(nlogn) time | O(1) space
fun smallestDifference(arrayOne: MutableList<Int>, arrayTwo: MutableList<Int>): List<Int> {
    var distance = 0
    var indexOne = 0
    var indexTwo = 0
    var results = listOf<Int>()
    
    arrayOne.sort()
    arrayTwo.sort()
    distance = abs(arrayOne[0] - arrayTwo[0])
    while (indexOne < arrayOne.size && indexTwo < arrayTwo.size){
        val currentDistance = abs(arrayOne[indexOne] - arrayTwo[indexTwo])
        if(currentDistance < distance){
            distance = currentDistance
            results = listOf(arrayOne[indexOne], arrayTwo[indexTwo])
        }
        if(arrayOne[indexOne] < arrayTwo[indexTwo]){
            indexOne ++
        }else{
            indexTwo ++
        }
    }
    return results
}

```


#### 8.Move Element To End
**Solution 1**
```Kotlin
// O(n) time | O(n) space
fun moveElementToEnd(array: MutableList<Int>, toMove: Int): List<Int> {
    if (array.size == 0) return array
    val results = mutableListOf<Int>()
    var count = 0

    array.forEach {
        if (it != toMove){
            results.add(it)
            count ++
        }
    }
    for (i in 0 until array.size - count){
        results.add(toMove)
    }
    return results
}
```


#### 9.Monotonic Array
**Solution 1**
```Kotlin
// O(n) time | O(1) space
fun isMonotonic(array: List<Int>): Boolean {
    // Write your code here.
    if (array.size < 3) return true

    var isInitialized = false
    var isIncreasing: Boolean? = null
    for (i in 0..array.size - 2){
        val currentIncrease: Boolean = if (array[i + 1] > array[i]){
            true
        }else if(array[i + 1] < array[i]){
            false
        }else{
            continue
        }
        if(!isInitialized){
            isIncreasing = currentIncrease
            isInitialized = true

        }else if(currentIncrease != isIncreasing){
            return false
        }
    }

    return true
}
```

**Solution 2**
```Kotlin
// O(n) time | O(1) space
fun isMonotonic(array: List<Int>): Boolean {
    if (array.size <= 2) return true
    var isIncreasing = true
    var isDecreasing = true

    for (i in 0..array.size - 2){
        if (array[i + 1] > array[i]){
            isDecreasing = false
        }
        if (array[i + 1] < array[i]){
            isIncreasing = false
        }
    }
	// TT TF FT return true; FF return false
    return isIncreasing || isDecreasing
}
```

#### 10.Spiral Traverse
**Solution 1**
```Kotlin
// O(n) time | O(n) space
fun spiralTraverse(array: List<List<Int>>): List<Int> {
    var top= 0
    var bottom = array.size - 1
    var left = 0
    var right = array[0].size - 1
    var results = arrayListOf<Int>()

    while (top <= bottom && left <= right){
        for (i in left..right){
            results.add(array[top][i])
        }
        for (i in top + 1..bottom){
            results.add(array[i][right])
        }
        for (i in right - 1 downTo left){
            if (top == bottom) break
            results.add(array[bottom][i])
        }
        for (i in bottom - 1 downTo top + 1){
            if (left == right) break
            results.add(array[i][left])
        }
        top ++
        bottom --
        left ++
        right --
    }
    return results
}
```

#### 11.Longest Peak
**Solution 1**
```Kotlin

// O(n) time | O(1) space
// O(n) time since the covered elements in the while loop are monotonous, so that doesn't 
// meet the condition of for loop outside
fun longestPeak(array: List<Int>): Int {
    if (array.size < 3) return 0
    var currentLong = 0
    var maxLong = 0
    
    for (i in 1..array.size - 2){
        if (array[i-1] < array[i] && array[i+1] < array[i]){
            currentLong ++
            var left = i - 1
            var right = i + 1

            while (left >= 0 && array[left] < array[left+1]){
                currentLong ++
                left --
            }
            while (right < array.size && array[right] < array[right-1]){
                currentLong ++
                right ++
            }
            maxLong = max(currentLong, maxLong)
            currentLong = 0
        }
    }
    return maxLong
}


```

#### 12.Array Of Product
**Solution 1**
```Kotlin
// O(n) time | O(n) space
fun arrayOfProducts(array: List<Int>): List<Int> {
    val results = arrayListOf<Int>()
    var product = 1

    product = production(array)
    array.forEach {
        if (it != 0)
            results.add(product / it)
        else{
            val temArray = array.toMutableList()
            temArray.remove(0)
            results.add(production(temArray))
        }
    }
    return results
}

fun production(array: List<Int>): Int{
    var product = 1
    array.forEach {
        product *= it
    }
    return product
}
```

#### 13.First Duplicate Value
**Solution 1**
```Kotlin
//O(n) time | O(1) space
fun firstDuplicateValue(array: MutableList<Int>): Int {
    var minIndex = array.size - 1
    var result = -1

    for (i in 0 until array.size){
        if (i > minIndex) break
        val item = array[0]
        array.remove(item)
        if (array.contains(item) && array.indexOf(item) + i < minIndex){
            result = item
            minIndex = array.indexOf(item) + i
        }
    }
    return result
}

```

#### 14.Merge Overlapping Intervals
**Solution 1**
```Kotlin
// O(n^2) time | O(n) space
fun mergeOverlappingIntervals(intervals: List<List<Int>>): List<List<Int>> {
    val results = arrayListOf<List<Int>>()
    val interval = intervals.toMutableList()

    for (i in interval.indices){
        var isOverlap = false
        for(j in i+1 until interval.size){
            if(isOverlap(interval[i], interval[j])){
                isOverlap = true
                interval[j] = mergeInterval(interval[i], interval[j])
            }
        }
        if (!isOverlap) results.add(interval[i])
    }
    return results
}

fun isOverlap(intervalOne: List<Int>, intervalTwo: List<Int>): Boolean{
    return (intervalOne[1] >= intervalTwo[0] && intervalOne[1] <= intervalTwo[1])||
            (intervalTwo[1] >= intervalOne[0] && intervalTwo[1] <= intervalOne[1])
}

fun mergeInterval(intervalOne: List<Int>, intervalTwo: List<Int>): List<Int>{
    return listOf(min(intervalOne[0], intervalTwo[0]), max(intervalOne[1], intervalTwo[1]))
}

```

**Solution 2**
```Kotlin
// O(nlogn) time and O(n) space
fun mergeOverlappingIntervals(intervals: List<List<Int>>): List<List<Int>> {
    var index = 0
    var tempInterval: List<Int>
    var results = mutableListOf<List<Int>>()
    var sortedIntervals = intervals.toMutableList().sortedWith(Comparator { i1, i2 ->  i1[0].compareTo(i2[0])})

    tempInterval = sortedIntervals[0]
    while (index < sortedIntervals.size - 1){
        if (tempInterval[1] >= sortedIntervals[index+1][0]){
            tempInterval = listOf(min(tempInterval[0], sortedIntervals[index+1][0]), max(tempInterval[1], sortedIntervals[index+1][1]))
        }else{
            results.add(tempInterval)
            tempInterval = sortedIntervals[index+1]
        }
        index ++
    }
    results.add(tempInterval)
    return results
}
```


#### 15.Four Number Sum
**Solution 1**
```Kotlin

// O(n^3) time and O(n) space
fun fourNumberSum(array: MutableList<Int>, targetSum: Int): List<List<Int>> {
    var results = mutableListOf<List<Int>>()
    var indexOne = 0; var indexTwo = 1; var indexThree = 3; var indexFour = 4
    if (array.size < 4) return listOf()

    array.sort()

    while (array.size > 3){
        val temp = array[0]
        array.removeAt(0)
        val threeNumList = threeNumberSum(array.toMutableList(), targetSum - temp)
        threeNumList.forEach {
            results.add(listOf(temp, it[0], it[1], it[2]))
        }
    }
    return results
}

fun threeNumberSum(array: MutableList<Int>, targetSum: Int): List<List<Int>>{
    val results = mutableListOf<List<Int>>()

    while (array.size > 2){
        val temp = array[0]
        array.removeAt(0)
        val twoNumList = twoNumSum(array.toMutableList(), targetSum - temp)
        if (twoNumList.isNotEmpty()){
            twoNumList.forEach {
                results.add(listOf(temp, it[0], it[1]))
            }
        }
    }

    return results
}

fun twoNumSum(array: MutableList<Int>, targetSum: Int): List<List<Int>>{
    val results = mutableListOf<List<Int>>()

    while (array.size > 1){
        val temp = array[0]
        array.removeAt(0)
        if (array.contains(targetSum - temp)){
            results.add(listOf(temp, targetSum - temp))
            array.remove(targetSum - temp)
        }
    }

    return results
}
```

#### 16.Subarray Sort
**Solution 1**
```Kotlin
// O(n) time | O(1) space
fun subarraySort(array: List<Int>): List<Int> {
    var leftIdx = 0
    var rightIdx = array.size - 1
    var localMax = 0
    var localMin = 0

    while (leftIdx < rightIdx){
        if (array[leftIdx] > array[leftIdx+1] && array[rightIdx-1] > array[rightIdx]) break
        if(rightIdx - leftIdx <= 1) return listOf<Int>(-1, -1)
        if (array[leftIdx] <= array[leftIdx+1]) leftIdx ++
        if (array[rightIdx-1] <= array[rightIdx]) rightIdx --
    }
    localMax = array[rightIdx]
    localMin = array[leftIdx]
    for (i in leftIdx..rightIdx){
        localMax = max(localMax, array[i])
        localMin = min(localMin, array[i])
    }
    while (leftIdx > 0 && array[leftIdx-1] > localMin){
        leftIdx --
    }
    while (rightIdx < array.size - 1 && array[rightIdx+1] < localMax){
        rightIdx ++
    }

    return listOf<Int>(leftIdx, rightIdx)
}
```


#### 17.Largeset Range
**Solution 1**
```Kotlin
// O(nlogn) time and O(1) space
fun largestRange(array: List<Int>): Pair<Int, Int> {
    if(array.size == 1) return Pair(array[0], array[0])
    var leftIdx = 0
    var rightIdx = 0
    var currentRange = 1
    var maxRange = 1
    var start = 0

    val sortedArray = array.toMutableList()
    sortedArray.sort()
    while (rightIdx < sortedArray.size - 1){
        if (sortedArray[rightIdx+1] <= sortedArray[rightIdx] + 1){
            currentRange = rightIdx + 1 - leftIdx
        } else {
            leftIdx = rightIdx + 1
        }
        if (currentRange > maxRange){
            if(sortedArray[start] < sortedArray[start+currentRange]){
                maxRange = currentRange
            }
            start = leftIdx
        }
        rightIdx ++
    }
    return Pair(sortedArray[start], sortedArray[start+maxRange])
}
```



#### 18.Min Rewards
**Solution 1**
```kotlin
// O(nlogn) time and O(n) space
fun minRewards(scores: List<Int>): Int {
    val sortedScores = scores.toMutableList()
    val rewards = arrayListOf<Int>()

    if (scores.size == 1) return 1
    for (i in scores.indices) rewards.add(1)
    sortedScores.sort()
    sortedScores.forEach {
        val index = scores.indexOf(it)
        if (index > 0 && index < scores.size - 1){
            if (scores[index-1] > it) 
                rewards[index-1] = max(rewards[index] + 1, rewards[index-1])
            if (scores[index+1] > it)
                rewards[index+1] = max(rewards[index] + 1, rewards[index+1])
        }
    }
    if (scores[0] > scores[1]) 
        rewards[0] = rewards[1] + 1
    if (scores[scores.size - 1] > scores[scores.size - 2]) 
        rewards[scores.size - 1] = rewards[scores.size - 2] + 1
    return rewards.sum()
}
```

**Solution 2**
```kotlin
// O(n) time | O(n) space
fun minRewards(scores: List<Int>): Int {
    val rewards = MutableList(scores.size){1}
    if (scores.size == 1) return 1
    if (scores.size == 2) return 3
    for (i in 1..scores.size - 2){
        if(scores[i] < scores[i - 1] && scores[i] < scores[i + 1]){
            var left = i - 1
            var right = i + 1
            while (left >= 0 && scores[left] > scores[left+1]){
                rewards[left] = max(rewards[left+1] + 1, rewards[left])
                left --
            }
            while (right <= scores.size - 1 && scores[right] > scores[right-1]){
                rewards[right] = max(rewards[right-1] + 1, rewards[right])
                right ++
            }
        }
    }
    return rewards.sum()
}
```


**Solution 3**
```kotlin
// O(n) time | O(n) space
fun minRewards(scores: List<Int>): Int {
    val rewards = MutableList(scores.size){1}
    if (scores.size == 1) return 1
    if (scores.size == 2) return 3
    for (i in 1 until scores.size){
        if (scores[i] > scores[i-1]) rewards[i] = max(rewards[i-1] + 1, rewards[i])
    }
    for (i in scores.size - 2 downTo 0){
        if (scores[i] > scores[i+1]) rewards[i] = max(rewards[i+1] + 1, rewards[i])
    }
    return rewards.sum()
}
```



#### 19.Zigzag Traverse
```kotlin
// O(n) time | O(n) space
fun zigzagTraverse(array: List<List<Int>>): List<Int> {
    val width = array[0].size - 1
    val height = array.size - 1
    var leftEnd = Pair(0, 0)
    var rightEnd = Pair(0, 0)
    var isFromLeft = false
    val results = mutableListOf<Int>()

    for (i in 0..width + height){
        val count = rightEnd.second - leftEnd.second
        for (j in 0..count){
            if (isFromLeft){
                results.add(array[leftEnd.first - j][leftEnd.second + j])
            }else{
                results.add(array[rightEnd.first + j][rightEnd.second - j])
            }
        }
        isFromLeft = !isFromLeft
        leftEnd = if (leftEnd.first == height)
            Pair(height, leftEnd.second + 1)
        else
            Pair(leftEnd.first + 1, 0)
        rightEnd = if (rightEnd.second == width)
            Pair(rightEnd.first + 1, width)
        else
            Pair(0, rightEnd.second + 1)

    }
    return results
}
```

<a name="Part2"></a>
### Binary Search Tree

#### 1.Find Closest Value in BST
```kotlin
open class BST(value: Int) {
    var value = value
    var left: BST? = null
    var right: BST? = null
}

var valueOne = 0
var valueTwo = 0
// Average O(logn) time | O(logn) space
// Worst O(n) time | O(n) space
fun findClosestValueInBst(tree: BST, target: Int): Int {
    var result = 0
    if(tree.left != null){
        result = findClosestValueInBst(tree.left!!, target)
        if(result > target) return result
    }
    if(tree.value < target) valueOne = tree.value
    else valueTwo = tree.value

    if (valueTwo != 0){
        return if(abs(valueOne - target) < abs(valueTwo - target)) valueOne
        else valueTwo
    }
    if(tree.right != null){
        result = findClosestValueInBst(tree.right!!, target)
        if(result > target) return result
    }
    return result
}
```
