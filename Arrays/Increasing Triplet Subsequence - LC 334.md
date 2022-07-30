Ok, so I read the description again, then I realize, it is asking about some sort of "increasing subsequence" with size 3.

Then I think about all the relevant algorithm I know, for example, the famous "Longest Increasing Subsequence" (LIS) problem.

Then I instantly got a solution: Find the LIS of the input, and if it is greater than 3, return true;  
Looks like a working solution, what's its complexity then:

There is a O(nlogk) solution to LIS (if you don't know it, just search this problem in Leetcode and see the discussions), where n is the array length and k is the length of LIS. Here, k is no larger than 2, so it is O(nlog2) = O(n). Very well, a O(n) solution is so easily obtained here:
