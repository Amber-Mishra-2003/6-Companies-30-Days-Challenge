# Sort an Array

Problem Link :- [Link](https://leetcode.com/problems/sort-an-array/)

<h3>
Problem :- Given an array of integers nums, sort the array in ascending order and return it.

You must solve the problem without using any built-in functions in O(nlog(n)) time complexity and with the smallest space complexity possible.
</h3>


**Solution :-**
```
class Solution {
public:
    
    vector<int> sortArray(vector<int>& nums) {
       
         vector<int> negnums, posnums;
        
         for(auto i:nums){
            if(i<0) negnums.push_back(-1*i);
            else posnums.push_back(i);
        }
        if(negnums.size()>0) radixsort(negnums);
        if(posnums.size()>0) radixsort(posnums);
        
        int j=0;
        for(int i=negnums.size()-1;i>=0;i--){
            nums[j]=-1*negnums[i];
            j++;
        }
        
        for(int i=0;i<posnums.size();i++){
            nums[j]=posnums[i];
            j++;
        }
        return nums;
        
        
    }
    
    void radixsort(vector<int> &nums){

        vector<int>::iterator it=max_element(nums.begin(),nums.end());
        int max=*it;
        for(int i=1;(max/i)>0;i*=10){
            countsort(nums,i);
        }
        
    }
        
        
        void countsort(vector<int>& nums,int idx){
            // all values are from 0-9
            vector<int>count(10);
            for(int i=0;i<nums.size();i++){
                count[(nums[i]/idx)%10]++;
            }
            
    
            for(int i=1;i<count.size();i++){
                count[i]=count[i-1]+count[i];
            }
            
           
            vector<int> nums2(nums.size());
            for(int i=nums.size()-1;i>=0;i--){
                nums2[--count[(nums[i]/idx)%10]]=nums[i];  
            }
          
            for(int i=0;i<nums2.size();i++){
                nums[i]=nums2[i];
            }
          
            
        }
};
```
