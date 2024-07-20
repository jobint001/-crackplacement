There are several cards arranged in a row, and each card has an associated number of points. The points are given in the integer array cardPoints.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly k cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array cardPoints and the integer k, return the maximum score you can obtain.

 

Example 1:

Input: cardPoints = [1,2,3,4,5,6,1], k = 3
Output: 12
Explanation: After the first step, your score will always be 1. However, choosing the rightmost card first will maximize your total score. The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.

# Approach
- Step-1: Firstly calculate the sum of First K Elements

- Step-2: Then for last K elements, we will do it by removing one element one by one from First K elements and including elements one by one from last.

- Step-3: Take Two Pointers:

 Left Index on - k-1th Index.
Right Index on - n-1th Index
- Step-3:
Now we will do 3 steps simultaneously in every iteration :

Decrease the size from Window of 1st Kth Elements
Increase the size in the window of Last Kth Elements
Check if the current total sum is greater than the maxSum. If YES, then update the maxSum.


```
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int n = cardPoints.size();

        // * Firstly, figure out the sum of 1st Kth elements
        int leftSum = 0, rightSum = 0, maxSum = 0;
        for(int i = 0; i < k; i++) 
            leftSum += cardPoints[i];
        // * Initially, out maxSum becomes left Sum
        maxSum = leftSum;

        for(int leftIdx = k-1, rightIdx = n-1; leftIdx >= 0; leftIdx--, rightIdx--){
            // * Shrink from START (leftIdx)
            leftSum -= cardPoints[leftIdx];
            //  * Increase size from END (rightIdx)
            rightSum += cardPoints[rightIdx];
            maxSum = max(maxSum, leftSum + rightSum);
        }

        return maxSum;
    }
};
```
