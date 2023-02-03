---
title: LeetCode 比赛记录
date: 2022-06-26 13:28:25
tags: 
  - LeetCode
---

记录一下LeetCode的VP和正式赛的情况，主要是训练一下反应速度，别总被傻逼题卡。

<!-- more-->

## Overview

| Contest ID                                                   | rank | Total   | T1          | T2          | T3          | T4          | Date       |
| ------------------------------------------------------------ | ---- | ------- | ----------- | ----------- | ----------- | ----------- | ---------- |
| [Weekly Contest 282](https://leetcode.com/contest/weekly-contest-282) | 283  | 0:55:09 | 0:00:42     | 0:04:17     | 0:05:15 (1) | 0:50:09     | 2022/06/08 |
| [Weekly Contest 281](https://leetcode.com/contest/weekly-contest-281) | 203  | 0:43:25 | 0:01:02     | 0:03:49     | 0:18:11     | 0:38:25 (1) | 2022/06/09 |
| [Biweekly Contest 80](https://leetcode.com/contest/biweekly-contest-80) | 153  | 0:27:26 | 0:02:22     | 0:05:16     | 0:18:48 (1) | 0:22:26     | 2022/06/11 |
| [Weekly Contest 297](https://leetcode.com/contest/weekly-contest-297) | 984  | 0:19:16 | 0:02:31     | 0:08:18     | 0:14:16 (1) |             | 2022/06/12 |
| [Weekly Contest 279](https://leetcode.com/contest/weekly-contest-279) | 523  | 1:12:34 | 0:02:17     | 0:05:52     | 0:37:43 (3) | 0:52:34 (1) | 2022/06/16 |
| [Biweekly Contest 71](https://leetcode.com/contest/biweekly-contest-71) | 217  | 1:01:57 | 0:01:25     | 0:05:26 (1) | 0:33:39 (3) | 0:41:57     | 2022/06/16 |
| [Weekly Contest 278](https://leetcode.com/contest/weekly-contest-278) | 126  | 1:00:18 | 0:01:26     | 0:08:07 (1) | 0:20:52     | 0:45:18 (2) | 2022/06/16 |
| [Weekly Contest 277](https://leetcode.com/contest/weekly-contest-277) | 29   | 0:09:40 | 0:01:37     | 0:03:38     | 0:05:03     | 0:09:40     | 2022/06/17 |
| [Biweekly Contest 70](https://leetcode.com/contest/biweekly-contest-70) | 287  | 0:54:41 | 0:04:11 (1) | 0:07:30 (2) | 0:18:03 (1) | 0:29:41 (1) | 2022/06/17 |
| [Weekly Contest 299](https://leetcode.com/contest/weekly-contest-299) | 175  | 0:48:51 | 0:03:02 (1) | 0:08:12     | 0:14:53     | 0:33:51 (2) | 2022/06/26 |
| [Biweekly Contest 81](https://leetcode.com/contest/biweekly-contest-81) | 168  | 0:29:18 | 0:01:30     | 0:07:49     | 0:09:23     | 0:29:18     | 2022/07/02 |
| [Weekly Contest 300](https://leetcode.com/contest/weekly-contest-300) | 42   | 0:23:46 | 0:01:58     | 0:06:52     | 0:13:55     | 0:23:46     | 2022/07/03 |
| [Biweekly Contest 82](https://leetcode.com/contest/biweekly-contest-82) | 47   | 0:49:40 | 0:01:36     | 0:10:05 (1) | 0:29:08     | 0:44:40     | 2020/07/09 |
| [Weekly Contest 301](https://leetcode.com/contest/weekly-contest-301) | 501  | 0:18:42 | 0:18:42     | 0:03:59     | 0:09:49     |             | 2020/07/10 |
| [Weekly Contest 302](https://leetcode.com/contest/weekly-contest-302) | 81   | 0:15:17 | 0:01:30     | 0:03:30     | 0:15:17     | 0:06:50     | 2020/07/17 |

## Summary

### Weekly Contest 279

前两题的速度还可以，6分钟过了T1、T2，排到第一页问题不大。

T3：总想搞事情，去试一些暴力的、目测就过不了的做法。实际上正解写起来快的很，浪费了得有20多分钟和3次罚时。

T4：边界情况考虑不周（尤其是处理后的vector大小为0的情况），有的时候开始想到了没写，最后就忘了，多了一次罚时。

T4还是做麻烦了，感觉有的时候还是没想清楚就去写，最后反而浪费时间。

对比一下VP时的T4和赛后的T4，思路基本是相同的，后者短的多，甚至天然都不会考虑边界情况：

```cpp
class Solution { // before
public:
    int minimumTime(string s) {
        vector<int> v;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '1')
                v.push_back(i);
        }
        int m = v.size();
        if (!m) return 0;
        auto f = vector(m, static_cast<int>(1e8));
        auto g = vector(m, static_cast<int>(1e8));
        if (v[0] != 0) {
            f[0] = 2;
        } else {
            f[0] = 1;
        }
        for (int i = 1; i < m; ++i) {
            f[i] = min(f[i - 1] + 2, v[i] + 1);
        }
        if (v[m - 1] != s.size() - 1) {
            g[m - 1] = 2;
        } else {
            g[m - 1] = 1;
        }
        for (int i = m - 2; i >= 0; --i) {
            g[i] = min(g[i + 1] + 2, (int)s.size() - v[i]);
        }
        int ans = min(f[m - 1], g[0]);
        for (int i = 0; i < m - 1; ++i)
            ans = min(ans, f[i] + g[i + 1]);
        return ans;
    }
};

class Solution { // after
public:
    int minimumTime(string s) {
        int pre = 0, ans = 1e9;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '1') {
                ans = min(ans, pre + (int)s.size() - i);
                pre = min(pre + 2, i + 1);
            }
        }
        return min(ans, pre);
    }
};
```

### Biweekly Contest 71

本场的核心问题就是读错题，T2、T3接连读错题，最离谱的是T3连着读错了好几次。（但我感觉这T3的题面写的也不够清楚，吗的）

感觉一方面英语阅读速度还是不够，另一方面可能还是有点着急。

这次T4的速度还可以，基本没卡壳，7min写完。

### Weekly Contest 278

T2诡异的错误，输入的是个vector我却把它当成string处理（'1'和1）。。

T3字符串哈希的定义没仔细看，写完才发现是和一般的规则是相反的，浪费了一些时间修改。

T4看了会儿群消息，应该再快个几分钟。

本来T4在第一发提交的时候把map改成了unordered_map，结果第一发发现读错题后，在VSCode里改的时候又忘了，白白T了一发。。

感觉这场专注度不够，今天就不再打了。

### Weekly Contest 277

深夜VP，没想到这次挺爽，10min内就全过了。

### Biweekly Contest 70

吗的不该开的，题目纯傻逼，下午图书馆热的要死，还困，写题质量极差，每题都能WA一发。

### Weekly Contest 299

吗的，真晕了，这是本来想着看中文题面会快一点，结果。。

T1因为if嵌套不加大括号，WA了一发。

T3感觉写麻烦了？

T4WA了两发，还是因为两个错误。。。

事实证明还是脑子转的不够快，加上手还有点问题。。

### Biweekly Contest 81

中规中矩吧，最后一题属于纯脑瘫了，一傻逼题写了20分钟，搞笑呢。不过至少这次没罚时，还凑合吧。

## Weekly Contest 300

这场还行，虽然还是慢了点，但至少没有脑溢血，应该是目前正式赛发挥的最好的一场了。
