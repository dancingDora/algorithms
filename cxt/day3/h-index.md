# h指数
给你一个整数数组 citations ，其中 citations[i] 表示研究者的第 i 篇论文被引用的次数。计算并返回该研究者的 h 指数。

根据维基百科上 h 指数的定义：h 代表“高引用次数” ，一名科研人员的 h 指数 是指他（她）至少发表了 h 篇论文，并且 至少 有 h 篇论文被引用次数大于等于 h 。如果 h 有多种可能的值，h 指数 是其中最大的那个。
```
int hIndex(vector<int>& citations) {
        int size = citations.size();
        sort(citations.begin(), citations.end());
        // 0 1 3 5 6
        int h = 0;
        for(int i = size-1; i >= 0; i--) {
            if(h >= citations[i]) break;
            h++;
        }
        return h;
    }
```
思路：先对给出的数组进行排序
