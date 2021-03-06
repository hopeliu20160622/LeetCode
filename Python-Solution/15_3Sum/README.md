# 15 - 三数之和

## 题目描述
![problem](images/15.png)

<!-- more -->

>审题：
这个这个，似曾相识呀，诶不就是第一题两数之和嘛
[两数之和-传送门](https://rosevil1874.github.io/2018/04/05/1.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C/#more)
So，可不可以把“三数之和”问题改成“两数之和+X”捏。。。

## 方法一：利用“两数之和”
1. 计算将列表中每个数与几（target）相加的和为零；
2. 分别使用这个target作为两数之和问题中的target；
3. 去重之后将符合条件的结果加入返回数组。
```python
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        l = len(nums)
        ret = []
        for j in range(l):
            target = 0 - nums[j]
            tmp = {}
            for i, a in enumerate(nums):
                if i == j:
                    continue
                if target-a in tmp:
                    re = sorted( [nums[j], nums[tmp[target-a]], nums[i]] ) 
                    if re not in ret:
                        ret.append( re )
                else:
                    tmp[a] = i

        return ret
```
超时啦啊啊啊啊啊(눈‸눈)
![overtime](images/overtime.png)

## 方法二：双指针
1. 将数组排序；
2. 第一层循环遍历元素到倒数第三个【第一个数】；
3. 第二层循环使用双指针在剩余位置由两端向中间靠拢检查【后两个数】；
4. 符合条件且不重复的加入结果数组。

```pyhton
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        l = len(nums)
        nums.sort()
        ret = []

        for i in range(l - 2):
            # 去重
            if i > 0 and nums[i] == nums[i-1]:
                continue

            # 双指针归位！
            j, k = i + 1, l - 1
            while j < k:
                if nums[i] + nums[j] + nums[k] == 0:
                    ret.append( [nums[i], nums[j], nums[k]] )
                    j += 1
                    k -= 1

                    # 去重
                    while j < k and nums[j] == nums[j-1] :
                        j += 1
                    while j < k and nums[k] == nums[k+1] :
                        k -= 1
                elif nums[i] + nums[j] + nums[k] < 0:
                    j += 1
                else:
                    k -= 1

        return ret
```

还是超时，黑人问号.jpg
![黑人问号.jpg](images/黑人问号.jpg)

问题出在哪里，，，我把l = len(nums)去掉了，所有需要用到l的地方直接使用len(nums)就AC了，excuse me？？？把它暂存起来不是更快吗？？？看看这个卡住的测试用例吧：
![overtime2](images/overtime2.png)

**2018.04.19 review**
还是一样的代码，现在提交就通过了，简直。。。唉过了就好( ･´ω`･ )
