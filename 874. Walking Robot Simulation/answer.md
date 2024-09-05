A robot on an infinite XY-plane starts at point (0, 0) facing north. The robot can receive a sequence of these three possible types of commands:

-2: Turn left 90 degrees.
-1: Turn right 90 degrees.
1 <= k <= 9: Move forward k units, one unit at a time.
Some of the grid squares are obstacles. The ith obstacle is at grid point obstacles[i] = (xi, yi). If the robot runs into an obstacle, then it will instead stay in its current location and move on to the next command.

Return the maximum Euclidean distance that the robot ever gets from the origin squared (i.e. if the distance is 5, return 25).

Note:

North means +Y direction.
East means +X direction.
South means -Y direction.
West means -X direction.
There can be obstacle in [0,0].
 

Example 1:

Input: commands = [4,-1,3], obstacles = []
Output: 25
Explanation: The robot starts at (0, 0):
1. Move north 4 units to (0, 4).
2. Turn right.
3. Move east 3 units to (3, 4).
The furthest point the robot ever gets from the origin is (3, 4), which squared is 32 + 42 = 25 units away.
Example 2:

Input: commands = [4,-1,4,-2,4], obstacles = [[2,4]]
Output: 65
Explanation: The robot starts at (0, 0):
1. Move north 4 units to (0, 4).
2. Turn right.
3. Move east 1 unit and get blocked by the obstacle at (2, 4), robot is at (1, 4).
4. Turn left.
5. Move north 4 units to (1, 8).
The furthest point the robot ever gets from the origin is (1, 8), which squared is 12 + 82 = 65 units away.

```
class Solution {
public:
    int robotSim(vector<int>& commands, vector<vector<int>>& obstacles) {
        unordered_map<string,int>mp;
        for(auto it:obstacles){
            string key = to_string(it[0])+"+"+to_string(it[1]);
            mp[key]++;
        }
        vector<vector<int>>direc = {{-1,0},{0,1},{1,0},{0,-1}}; 
        // according to order W N E S

        int dir = 1; // i.e. north 
        // 0: west, 1: north, 2: east, 3: south
        int x=0,y=0;
        int mxDist=0;
        for(int it:commands){
            if(it==-2){
                // move left
                if(dir==0) dir = 3;
                else dir--;
            }
            else if(it==-1){
                // move right
                dir = (dir+1)%4;
            }
            else{
                int k = it;
                for(int i=1; i<=k; i++){
                    int newX = x+direc[dir][0];
                    int newY = y+direc[dir][1];
                    
                    string key = to_string(newX)+"+"+to_string(newY);
                    if(mp.find(key)!=mp.end()){
                        // obstacle has been found so don't go there
                        break;
                    }
                    x = newX, y=newY;
                    mxDist = max(mxDist, x*x+y*y);
                }
            }
        } 

        return mxDist;


    }
};
```