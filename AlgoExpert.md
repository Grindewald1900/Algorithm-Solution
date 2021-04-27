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
