# Count Good Triplets in an Array

Problem Link :- [Link](https://leetcode.com/problems/count-good-triplets-in-an-array/)

<h3>
Problem :- You are given two 0-indexed arrays nums1 and nums2 of length n, both of which are permutations of [0, 1, ..., n - 1].

A good triplet is a set of 3 distinct values which are present in increasing order by position both in nums1 and nums2. In other words, if we consider pos1v as the index of the value v in nums1 and pos2v as the index of the value v in nums2, then a good triplet will be a set (x, y, z) where 0 <= x, y, z <= n - 1, such that pos1x < pos1y < pos1z and pos2x < pos2y < pos2z.

Return the total number of good triplets.
</h3>


**Solution :-**
```
class segtree {
	int size;
	vector<long long> sums;
public:
	segtree(int n) {
		size = 1;
		while(size < n)
			size *= 2;
		sums = vector<long long>(2 * size - 1);
	}
	void set(int i, int val, int x, int l, int r) {
		if(l == r) {
			sums[x] = val;
			return;
		}
		int mid = (l + r) / 2;
		if(i <= mid)
			set(i, val, 2 * x + 1, l, mid);
		else
			set(i, val, 2 * x + 2, mid + 1, r);
		sums[x] = sums[2 * x + 1] + sums[2 * x + 2];
	}
	void set(int i, int val) {
		set(i, val, 0, 0, size -1);
	}
	long long  range_sum(int lx, int rx, int x, int l, int r) {
		if(l > rx || lx > r)
			return 0;
		if(l >= lx && r <= rx)
			return sums[x];
		int mid = (l + r) / 2;
		return range_sum(lx, rx, 2 * x + 1, l, mid) + range_sum(lx, rx, 2 * x + 2, mid + 1, r);
	}
	long long  range_sum(int lx, int rx) {
		return range_sum(lx, rx, 0, 0, size - 1);
	}
};


class Solution {
public:
    long long goodTriplets(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        vector<int> pos1(n);
        vector<int> pos2(n);
        for (int i = 0; i < n; i++) {
            pos1[nums1[i]] = i;
            pos2[nums2[i]] = i;
        }
        vector<pair<int, int>> put;
        for (int i = 0; i < n; i++) {
            put.emplace_back(pos1[i], pos2[i]);
        }
        sort(put.begin(), put.end());
        vector<int> less(n);
        segtree st(n);
        for (int i = 0; i < n; i++) {
            less[i] = st.range_sum(0, put[i].second);
            st.set(put[i].second, 1);
        }
        segtree st1(n);
        long long sol = 0;
        for (int i = n - 1; i >= 0; i--) {
            int v = st1.range_sum(put[i].second, n - 1);
            st1.set(put[i].second, 1);
            sol += (long long) less[i] * v;
        }
        return sol;
        
    }
};
```
