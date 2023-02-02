# Number of Pairs Satisfying Inequality

Problem Link :- [Link](https://leetcode.com/problems/number-of-pairs-satisfying-inequality/)

<h3>
Problem :- You are given two 0-indexed integer arrays nums1 and nums2, each of size n, and an integer diff. Find the number of pairs (i, j) such that:

  
  
0 <= i < j <= n - 1 and nums1[i] - nums1[j] <= nums2[i] - nums2[j] + diff.
  
Return the number of pairs that satisfy the conditions.

</h3>



**Solution :-**

```
class Solution {
public:
    
    vector<vector<int>> seg;
    
    vector<int> merge(vector<int>& v1, vector<int>& v2){
        int n = v1.size();
        int m = v2.size();
        vector<int> temp(n+m);
        int i = 0;
        int j = 0;
        for(int k = 0; k<n+m; k++){
            if(i == n){
                temp[k] = v2[j++];
            }
            else if(j == m){
                temp[k] = v1[i++];
            }
            else{
                if(v1[i] < v2[j]){
                    temp[k] = v1[i++];
                }
                else{
                    temp[k] = v2[j++];
                }
            }
        }
        return temp;
    }
    
    void build_tree(int N, int l, int r, vector<int>& v){
        if(l == r){
            seg[N].push_back(v[l]);
            return;
        }
        
        int mid = (l+r)/2;
        
        build_tree(2*N, l, mid, v);
        build_tree(2*N+1, mid+1, r, v);
        
        seg[N] = merge(seg[2*N], seg[2*N+1]);
    }
    
    int query_tree(int i, int j, int num, int N, int l, int r){
        if(r<i or l>j) return 0;
        if(l>=i and r<=j){
            int idx = upper_bound(seg[N].begin(), seg[N].end(), num) - seg[N].begin();
            return idx;
        }
        
        int mid = (l+r)/2;
        
        int n1 = query_tree(i, j, num, 2*N, l, mid);
        int n2 = query_tree(i, j, num, 2*N+1, mid+1, r);
        
        return n1 + n2;
    }
    
    long long numberOfPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        int n = nums1.size();
        vector<int> diff(n);
        seg.resize(4*n);
        long long cnt = 0;
        for(int i = 0; i<n; i++){
            diff[i] = nums1[i] - nums2[i];
        }
        build_tree(1, 0, n-1, diff);
        for(int i = 0; i<n; i++){
            cnt += query_tree(0, i-1, diff[i] + k, 1, 0, n-1);
            
        }
        
        
        return cnt;
    }
};
```
