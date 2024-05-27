# 多数元素
给定一个大小为 n 的数组 nums ，返回其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

### 法1： 利用hash表

```
int majorityElement(vector<int>& nums) {
        int size = nums.size();
        unordered_map<string, int> mp;

        for(int i = 0; i < size; i++) {
            string tmp = to_string(nums[i]);
            if(mp.find(tmp) == mp.end()) {
                mp.insert(pair<string,int>(tmp,1));
            } else {
                mp[tmp] ++;
            }
        }
        int res = 0;
        for(const auto& m: mp) {
            if(m.second > size / 2) {
                res = stoi(m.first);
            }
        }
        return res;
    }
```

或是：
```
int majorityElement(vector<int>& nums) {
        unordered_map<int, int> counts;
        int majority = 0, cnt = 0;
        for(const int& num: nums) {
            ++counts[num];
            if(counts[num] > cnt) {
                majority = num;
                cnt = counts[num];
            }
        }
        return majority;
    }
```

改进之处：我们用一个循环遍历数组 nums 并将数组中的每个元素加入哈希映射中。在这之后，我们遍历哈希映射中的所有键值对，返回值最大的键。我们同样也可以在遍历数组 
nums 时候使用打擂台的方法，维护最大的值，这样省去了最后对哈希映射的遍历。

**复杂度分析：**
* 时间复杂度： `O(N)`
* 空间复杂度： `O(N)`

### 法2： 排序
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
};
```
* 时间复杂度： `O(logn)`
* 空间复杂度： `O(logn)`

### 法3： Boyer-Moore投票算法（官方题解）
```
int majorityElement(vector<int>& nums) {
        int candidate = -1;
        int count = 0;
        for (int num : nums) {
            if (num == candidate)
                ++count;
            else if (--count < 0) {
                candidate = num;
                count = 1;
            }
        }
        return candidate;
    }

```

