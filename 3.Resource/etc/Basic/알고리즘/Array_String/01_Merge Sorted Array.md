# 📌 문제명: Merge Sorted Array  
- 출처: [LeetCode]
- 난이도: [Easy]

---

## 🧠 문제 설명  
서로 다른 두 오름차순 배열이 존재 할 때, 두 배열을 오름차순 배열로 합치는 문제

---

## 🚧 풀이 전략  
1. 핵심 로직:
    - 배열에 값을 적절하게 잘 넣고, 오름차순 정렬
2. 시간 복잡도:
    - O(NlogN)  
3. 핵심 키워드:
    - 배열

---

## ✅ 최종 코드 (Python)

```python
class Solution(object):
	def merge(self, nums1, m, nums2, n):
		for i in range(n):
			nums1[m + i] = nums2[i]
		nums1.sort()
```

