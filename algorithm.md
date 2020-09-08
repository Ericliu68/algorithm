### 自己的算法练习记录

#### 1. 两个数组的交集（第350）

给定两个数组，编写一个函数计算他们的交集

**示例1：**

```
输入： nums1 = [1, 2, 2, 1], num2 = [2, 2]

输出： [2,2]
```

**示例2：**

```
输入： nums1 = [4, 9, 5], num2 = [9, 4, 9, 8, 4]

输出： [4, 9]
```

说明:
输出结果中每个元素出现的次数,应与元素在两个数组中出现的次数一致。
我们可以不考虑输出结果的顺序。
进阶:
如果给定的数组已经排好序呢?将如何优化你的算法呢?
思路:设定两个为0的指针,比较两个指针的元素是否相等。如果指针的元素相等,我们将两个指针一
起向后移动,并且将相等的元素放入空白数组。

**优秀解答**

```go
// 解法一， 针对所有列表
func intersect1(nums1 []int, nums2 []int) []int {
	m0 := map[int]int{}
	for _, v := range nums1{
		m0[v] += 1
	}
	k := 0
	for _, v := range nums2{
		if m0[v] > 0{
			m0[v] -= 1
			nums2[k] = v
			k++
		}
	}
	return nums2[0:k]
}

// 解法二: 针对有序的列表

func intersect2(nums1 []int, nums2 []int) []int {
	i, j, k := 0, 0, 0
	sort.Ints(nums1)
	sort.Ints(nums2)
	for i < len(nums1) && j < len(nums2){
		if nums1[i] > nums2[j] {
			j++
		} else if nums1[i] < nums2[j]{
			i++
		} else {
			nums1[k] = nums1[j]
			i++
			j++
			k++
		}
	}
	return nums[:k]
}

```

#### 2. 最长公共前缀（14）

编写一个函数来查找数组中最长的公共前缀，如果不存在公共前缀，则返回“”

**示例1：**

```
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例2：**

```
输入: ["dog","racecar","car"]
输出: ""
```



