You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

[Explanation](https://youtu.be/KhL8cnEk65A)


 

Answer:

- Assign two pointers left and right

- Calcualte area of the containter.

- Update maxArea
- move the pointer which is smaller because we want higher height to get more area



```

class Solution {
public:
    int maxArea(vector<int>& height) {

        int maxArea= 0,currArea=0,left=0,right=height.size()-1;
        while(left!=right){
            currArea=(min(height[left],height[right]))*(right-left);
            maxArea=max(maxArea,currArea);
            if(height[left]<=height[right]) left++;
            else right--;

        }
        return maxArea;
        
    }
};

```
