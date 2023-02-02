# Find in Mountain Array

Problem Link :- [Link](https://leetcode.com/problems/find-in-mountain-array/)

<h3>
Problem :- (This problem is an interactive problem.)

You may recall that an array arr is a mountain array if and only if:

  * arr.length >= 3
  
  * There exists some i with 0 < i < arr.length - 1 such that:
  
    * arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
    * arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
Given a mountain array mountainArr, return the minimum index such that mountainArr.get(index) == target. If such an index does not exist, return -1.

You cannot access the mountain array directly. You may only access the array using a MountainArray interface:

  * MountainArray.get(k) returns the element of the array at index k (0-indexed).
  
  * MountainArray.length() returns the length of the array.
  
Submissions making more than 100 calls to MountainArray.get will be judged Wrong Answer. Also, any solutions that attempt to circumvent the judge will result in disqualification.
</h3>


**Solution :-**
```
/**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * class MountainArray {
 *   public:
 *     int get(int index);
 *     int length();
 * };
 */

class Solution {
public:
    int peak_element(MountainArray &mountainArr){
        int low = 0,high= mountainArr.length()-1;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(mountainArr.get(mid)<mountainArr.get(mid+1)){
                low = mid + 1;
            } else{
                if(mountainArr.get(mid)>mountainArr.get(mid-1)){
                    return mid;
                } else{
                    high = mid - 1;
                }
            } 
        }
        return -1;
    }
    
    int searchElement_low(MountainArray &mountainArr,int low,int high,int target){
          while(low<=high){
              int mid = low +(high-low)/2;
              if(mountainArr.get(mid)==target){
                  return mid;
              } else if(mountainArr.get(mid)>target){
                  high = mid - 1;
              } else{
                  low = mid + 1;
              }
          }
          return -1;
    }
    
    int searchElement_high(MountainArray &mountainArr,int low,int high,int target){
          while(low<=high){
              int mid = low+(high-low)/2;
              if(mountainArr.get(mid)==target){
                  return mid;
              }
              else if(mountainArr.get(mid)>target){
                  low  = mid + 1;
              }
              else{
                  high = mid - 1;
              }
          }
          return -1;
    }
    int findInMountainArray(int target, MountainArray &mountainArr) {
      
        int n = mountainArr.length();   
        int p = peak_element(mountainArr);  
        
        int low_idx = searchElement_low(mountainArr,0,p,target);
        if(low_idx>=0){
            return low_idx;
        }
       
        int high_idx = searchElement_high(mountainArr,p+1,n-1,target);
        return high_idx; 
    }
};
```
