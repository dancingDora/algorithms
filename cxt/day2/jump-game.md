# 跳跃游戏
给你一个非负整数数组 nums ，你最初位于数组的 第一个下标 。数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标，如果可以，返回 true ；否则，返回 false 。

```
bool canJump(vector<int>& nums) {
        int size = nums.size();
        // 思路： 动态规划
        // dp[i]: 记录nums[i] 之前能达到的最远距离
        // dp[i] = max(dp[i-1], i+nums[i])
        vector<int> dp(size, 0);
        dp[0] = nums[0];
        for(int i = 1; i < size; i++) {
            if(i > dp[i-1]) return false;
            dp[i] = max(dp[i-1], i+nums[i]);
        }

        return true;
    }
};
```

