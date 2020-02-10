---
title: 【leetcode】4. 寻找两个有序数组的中位数
url: 421.html
id: 421
categories:
  - Linux &amp; VPS
date: 2019-05-20 16:55:45
tags:
---

题目描述：
-----

> 给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。 请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。 你可以假设 nums1 和 nums2 不会同时为空。

本人题解：
-----

> ![](https://images.fromling.com/images/1d5b9bb3bf021a6ee0dba56382e3ff0c.png)

    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) 
        {
            int m = nums1.size();
            int n = nums2.size();
            vector<int>::iterator miter = nums1.begin();
            vector<int>::iterator niter = nums2.begin();
            int count = 0;
    
            switch((m+n) % 2)
            {
                case 1:
                    {
                        vector<int>::iterator curriter;
                        while(miter != nums1.end() || niter != nums2.end())
                        {
                            if (miter != nums1.end() && niter != nums2.end())
                            {
                                curriter = (*miter) < (*niter)?miter++:niter++;
                            }
    
                            else if(miter != nums1.end())
                            {
                                curriter = miter++;
                            }
    
                            else if(niter != nums2.end())
                            {
                                curriter = niter++;
                            }
    
                            count ++;   
    
                            if (count == (m + n + 1) / 2)
                            {
                                return *curriter;
                            }
                        }
                    }
                    break;
                case 0:
                    {
                        vector<int>::iterator curriter = nums1.end();
                        vector<int>::iterator olditer = nums1.end();
                        while(miter != nums1.end() || niter != nums2.end())
                        {
                            olditer = curriter;
    
                            if (miter != nums1.end() && niter != nums2.end())
                            {
                                curriter = (*miter) < (*niter)?miter++:niter++;
                            }
    
                            else if(miter != nums1.end())
                            {
                                curriter = miter++;
                            }
    
                            else if(niter != nums2.end())
                            {
                                curriter = niter++;
                            } 
    
                            count ++;   
                            if (count == (m + n + 2) / 2)
                            {
                                return (double(*olditer) + double(*curriter)) / 2;
                            }
                        }
                    }
            }
    

dalao题解
-------

    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
            int mid = nums1.size() + nums2.size() ;
            int is_even = mid % 2;
            mid = mid / 2 + 1;
            double tmp = 0;
            int cur_1 = 0;
            int cur_2 = 0;
            for(int i = 0 ;i<mid;i++){
                int a = 0;
                if (cur_1 == nums1.size()){                
                    a = nums2[cur_2];
                    cur_2 ++;
                }else if (cur_2 == nums2.size()){
                    a = nums1[cur_1];
                    cur_1 ++;
                }else{
                    if (nums1[cur_1] < nums2[cur_2]){
                        a = nums1[cur_1];
                        cur_1 ++;
                    }else{
                        a = nums2[cur_2];
                        cur_2 ++;
                    }
                }
                if (is_even == 0 && i == mid - 2){
                    tmp += a;
                }else if (i == mid - 1){
                    tmp += a;
                }
            }
            if (is_even == 0){
                tmp = tmp / 2;
            }
            return tmp;
        }
    

收获
--

1.  `iterator`不可以赋值为`NULL`，不可以与`NULL`比较。如果想要起到类似的效果，可以赋值为`end()`
2.  dalao题解中关于中位数的判断很有意思，值得学习一下：设定temp，如果m+n为偶数，则提前两位进行相加，如果m+n为奇数，则只相加一次。避免了两个iterator的浪费