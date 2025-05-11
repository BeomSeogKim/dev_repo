# 📌 문제명: Merge Sorted Array  
- 출처: [LeetCode](https://leetcode.com/problems/remove-element/?envType=study-plan-v2&envId=top-interview-150)
- 난이도: [Easy]

---

## 🧠 문제 설명  
nums에 존재하는 원소 중 val과 같은 값들을 원소에서 제거해야 함

---

## 🚧 풀이 전략  
1. 핵심 로직:
    - Two Pointer
	    - 배열을 순회하며 변경해 주는 로직을 추가 
2. 시간 복잡도:
    - O(N)  
3. 핵심 키워드:
    - Two Pointer

---

## ✅ 최종 코드 (Python)

```python
class Solution(object):
	def removeElement(self, nums, val):
		writer = 0
		for reader in range(len(nums)):
			if nums[reader] != val:
				nums[writer] = nums[reader]
				writer += 1
		return writer
```
