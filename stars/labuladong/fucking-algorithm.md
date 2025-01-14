---
project: fucking-algorithm
stars: 126477
description: 刷算法全靠套路，认准 labuladong 就够了！English version supported! Crack LeetCode, not only how, but also why. 
url: https://github.com/labuladong/fucking-algorithm
---

English version is on labuladong.online too. Just enjoy：)

labuladong 的算法笔记
================

本仓库总共 60 多篇原创文章，都是基于 LeetCode 的题目，涵盖了所有题型和技巧，而且一定要做到**举一反三，通俗易懂**，绝不是简单的代码堆砌，后面有目录。

我先吐槽几句。**刷题刷题，刷的是题，培养的是思维，本仓库的目的就是传递这种算法思维**。我要是只写一个包含 LeetCode 题目代码的仓库，有个锤子用？没有思路解释，没有思维框架，顶多写个时间复杂度，那玩意一眼就能看出来。

只想要答案的话很容易，题目评论区五花八门的答案，动不动就秀 python 一行代码解决，有那么多人点赞。问题是，你去做算法题，是去学习编程语言的奇技淫巧的，还是学习算法思维的呢？你的快乐，到底源自复制别人的一行代码通过测试，已完成题目 +1，还是源自自己通过逻辑推理和算法框架不看答案写出解法？

网上总有大佬喷我，说我写的东西太基础，要么说不能借助框架思维来学习算法。我只能说大家刷算法就是找工作吃饭的，不是打竞赛的，我也是一路摸爬滚打过来的，我们要的是清楚明白有所得，不是故弄玄虚无所指。

不想办法做到通俗易懂，难道要上来先把《算法导论》吹上天，然后把人家都心怀敬仰地劝退？

**做啥事情做多了，都能发现套路的，我把各种算法套路框架总结出来，相信可以帮助其他人少走弯路**。我这个纯靠自学的小童鞋，花了一年时间刷题和总结，自己写了一份算法小抄，后面有目录，这里就不废话了。

在开始学习之前
-------

**1、先给本仓库点个 star，满足一下我的虚荣心**，文章质量绝对值你一个 star。我还在继续创作，给我一点继续写文的动力，感谢。

**2、建议收藏我的在线网站，每篇文章开头都有对应的力扣题目链接，可以边看文章边刷题，一共可以手把手带你刷 500 道题目**：

2024 最新地址：https://labuladong.online/algo/

GitHub Pages 地址：https://labuladong.online/algo/

Gitee Pages 地址：https://labuladong.gitee.io/algo/

labuladong 刷题全家桶简介
------------------

### 一、算法可视化面板

我的算法网站、所有配套插件都集成了一个算法可视化工具，可以对数据结构和递归过程进行可视化，大幅降低理解算法的难度。几乎每道题目的解法代码都有对应的可视化面板，具体参见下方介绍。

### 二、学习网站

内容当然是我的系列算法教程中最核心的部分，我的算法教程都发布在网站 labuladong.online 上，相信你会未来会在这里花费大量的学习时间，而不是仅仅加入收藏夹~

### 三、Chrome 插件

**主要功能**：Chrome 插件可以在中文版力扣或英文版 LeetCode 上快捷查看我的「题解」或「思路」，并添加了题目和算法技巧之间的引用关系，可以和我的网站/公众号/课程联动，给我的读者提供最丝滑的刷题体验。安装使用手册见下方目录。

### 四、vscode 插件

**主要功能**：和 Chrome 插件功能基本相同，习惯在 vscode 上刷题的读者可以使用该插件。安装使用手册见下方目录。

### 五、Jetbrains 插件

**主要功能**：和 Chrome 插件功能基本相同，习惯在 Jetbrains 家的 IDE（PyCharm/Intellij/Goland 等）上刷题的读者可以使用该插件。安装使用手册见下方目录。

最后祝大家学习愉快，在题海中自在遨游！

文章目录
====

### 本站简介

### 准备工作：安装刷题全家桶

-   配套 Chrome 刷题插件
-   配套 vscode 刷题插件
-   配套 JetBrains 刷题插件
-   算法可视化面板使用说明（必读）
-   使用可视化面板的 JS 基础（可选）
-   30 天刷题打卡挑战（可选）

### 极速入门：数据结构基础

-   本章导读
-   学习本站所需的 Java 基础
-   手把手带你实现动态数组
    -   数组（顺序存储）基本原理
    -   动态数组代码实现
-   手把手带你实现单/双链表
    -   链表（链式存储）基本原理
    -   链表代码实现
-   手把手带你实现队列/栈
    -   队列/栈基本原理
    -   用链表实现队列/栈
    -   环形数组技巧
    -   用数组实现队列/栈
    -   双端队列（Deque）原理及实现
-   手把手带你实现哈希表
    -   哈希表基本原理
    -   用拉链法实现哈希表
    -   线性探查法的两个难点
    -   线性探查法的两种代码实现
-   手把手带你实现哈希集合
    -   哈希集合的原理及代码实现
-   手写标准库中的二叉树结构
    -   二叉树基础及常见类型
    -   正在更新 ing
-   手把手带你实现二叉堆
    -   二叉堆的基本原理
    -   二叉堆的代码实现
-   正在更新 ing

### 第零章、核心框架汇总

-   本章导读
-   学习算法和刷题的框架思维
-   我的刷题心得：算法的本质
-   双指针技巧秒杀七道链表题目
-   双指针技巧秒杀七道数组题目
-   我写了首诗，把滑动窗口算法变成了默写题
-   我写了首诗，把二分搜索算法变成了默写题
-   东哥带你刷二叉树（纲领篇）
-   动态规划解题套路框架
-   回溯算法解题套路框架
-   回溯算法秒杀所有排列/组合/子集问题
-   球盒模型：回溯算法穷举的两种视角
-   BFS 算法解题套路框架
-   算法时空复杂度分析实用指南

### 第一章、手把手刷数据结构

-   手把手刷链表算法
    
    -   双指针技巧秒杀七道链表题目
    -   【强化练习】链表双指针经典习题
    -   递归魔法：反转单链表
    -   如何 K 个一组反转链表
    -   如何判断回文链表
-   手把手刷数组算法
    
    -   双指针技巧秒杀七道数组题目
    -   【强化练习】数组双指针经典习题
    -   一个方法团灭 nSum 问题
    -   小而美的算法技巧：前缀和数组
    -   【强化练习】前缀和技巧经典习题
    -   小而美的算法技巧：差分数组
    -   二维数组的花式遍历技巧
    -   滑动窗口算法核心代码模板
    -   【强化练习】滑动窗口算法经典习题
    -   滑动窗口算法延伸：Rabin Karp 字符匹配算法
    -   二分搜索算法核心代码模板
    -   实际二分搜索时的思维框架
    -   【强化练习】二分搜索算法经典习题
    -   带权重的随机选择算法
    -   田忌赛马背后的算法决策
    -   常数时间删除/查找数组中的任意元素
    -   一道数组去重的算法题把我整不会了
-   手把手刷二叉树算法
    
    -   东哥带你刷二叉树（纲领篇）
    -   东哥带你刷二叉树（思路篇）
    -   东哥带你刷二叉树（构造篇）
    -   东哥带你刷二叉树（后序篇）
    -   东哥带你刷二叉树（序列化篇）
    -   归并排序详解及应用
    -   东哥带你刷二叉搜索树（特性篇）
    -   东哥带你刷二叉搜索树（基操篇）
    -   东哥带你刷二叉搜索树（构造篇）
    -   快速排序详解及应用
    -   题目不让我干什么，我偏要干什么
    -   Git原理之最近公共祖先
    -   如何计算完全二叉树的节点数
    -   用栈模拟递归迭代遍历二叉树
-   手把手带你刷 100 道二叉树习题
    
    -   【强化练习】用「遍历」思维解题 I
    -   【强化练习】用「遍历」思维解题 II
    -   【强化练习】用「遍历」思维解题 III
    -   【强化练习】用「分解问题」思维解题 I
    -   【强化练习】用「分解问题」思维解题 II
    -   【强化练习】同时运用两种思维解题
    -   【强化练习】利用后序位置解题 I
    -   【强化练习】利用后序位置解题 II
    -   【强化练习】利用后序位置解题 III
    -   【强化练习】运用层序遍历解题 I
    -   【强化练习】运用层序遍历解题 II
    -   【强化练习】二叉搜索树经典例题 I
    -   【强化练习】二叉搜索树经典例题 II
-   手把手设计数据结构
    
    -   队列实现栈以及栈实现队列
    -   【强化练习】栈的经典习题
    -   【强化练习】队列的经典习题
    -   单调栈算法模板解决三道例题
    -   【强化练习】单调栈的几种变体及经典习题
    -   单调队列结构解决滑动窗口问题
    -   【强化练习】单调队列的通用实现及经典习题
    -   算法就像搭乐高：带你手撸 LRU 算法
    -   算法就像搭乐高：带你手撸 LFU 算法
    -   【强化练习】哈希表更多习题
    -   二叉堆详解实现优先级队列
    -   【强化练习】优先级队列经典习题
    -   一道求中位数的算法题把我整不会了
    -   前缀树算法模板秒杀五道算法题
    -   设计朋友圈时间线功能
    -   【强化练习】更多经典设计习题
-   手把手刷图算法
    
    -   图论基础及遍历算法
    -   环检测及拓扑排序算法
    -   众里寻他千百度：名流问题
    -   二分图判定算法
    -   并查集（Union-Find）算法
    -   Kruskal 最小生成树算法
    -   Prim 最小生成树算法
    -   Dijkstra 算法模板及应用

### 第二章、手把手刷动态规划

-   动态规划基本技巧
    
    -   动态规划解题套路框架
    -   动态规划设计：最长递增子序列
    -   最优子结构原理和 dp 数组遍历方向
    -   base case 和备忘录的初始值怎么定？
    -   动态规划穷举的两种视角
    -   动态规划和回溯算法的思维转换
    -   对动态规划进行降维打击
-   子序列类型问题
    
    -   经典动态规划：编辑距离
    -   动态规划设计：最长递增子序列
    -   动态规划设计：最大子数组
    -   经典动态规划：最长公共子序列
    -   动态规划之子序列问题解题模板
-   背包类型问题
    
    -   经典动态规划：0-1 背包问题
    -   经典动态规划：子集背包问题
    -   经典动态规划：完全背包问题
    -   目标和问题：背包问题的变体
-   用动态规划玩游戏
    
    -   动态规划之最小路径和
    -   动态规划帮我通关了《魔塔》
    -   动态规划帮我通关了《辐射4》
    -   旅游省钱大法：加权最短路径
    -   经典动态规划：正则表达式
    -   经典动态规划：高楼扔鸡蛋
    -   经典动态规划：戳气球
    -   经典动态规划：博弈问题
    -   经典动态规划：四键键盘
    -   一个方法团灭 LeetCode 打家劫舍问题
    -   一个方法团灭 LeetCode 股票买卖问题
-   贪心类型问题
    
    -   老司机加油算法
    -   贪心算法之区间调度问题
    -   扫描线技巧：安排会议室
    -   剪视频剪出一个贪心算法
    -   如何运用贪心思想玩跳跃游戏

### 第三章、必知必会算法技巧

-   经典暴力搜索算法
    
    -   回溯算法解题套路框架
    -   回溯算法秒杀所有排列/组合/子集问题
    -   球盒模型：回溯算法穷举的两种视角
    -   一文秒杀所有岛屿题目
    -   回溯算法最佳实践：解数独
    -   回溯算法最佳实践：括号生成
    -   回溯算法最佳实践：集合划分
    -   BFS 算法解题套路框架
    -   如何用 BFS 算法秒杀各种智力题
-   数学运算技巧
    
    -   一行代码就能解决的算法题
    -   几个反直觉的概率问题
    -   常用的位操作
    -   谈谈游戏中的随机算法
    -   讲两道常考的阶乘算法题
    -   如何高效寻找素数
    -   如何高效进行模幂运算
    -   如何同时寻找缺失和重复的元素
-   经典面试题
    
    -   算法笔试「骗分」套路
    -   一文秒杀所有丑数系列问题
    -   分治算法详解：运算优先级
    -   一个方法解决三道区间问题
    -   谁能想到，斗地主也能玩出算法
    -   烧饼排序算法
    -   字符串乘法计算
    -   如何实现一个计算器
    -   如何高效解决接雨水问题
    -   如何解决括号相关的问题
    -   如何判定完美矩形

感谢如下大佬参与翻译
==========

按照昵称字典序排名：

ABCpril, andavid, bryceustc, build2645, CarrieOn, cooker, Dong Wang, ExcaliburEX, floatLig, ForeverSolar, Fulin Li, Funnyyanne, GYHHAHA, Hi\_archer, Iruze, Jieyixia, Justin, Kevin, Lrc123, lriy, Lyjeeq, MasonShu, Master-cai, miaoxiaozui2017, natsunoyoru97, nettee, PaperJets, qy-yang, realism0331, SCUhzs, Seaworth, shazi4399, ShuozheLi, sinjoywong, sunqiuming526, Tianhao Zhou, timmmGZ, tommytim0515, ucsk, wadegrc, walsvid, warmingkkk, Wonderxie, wsyzxxxx, xiaodp, youyun, yx-tan, Zero, Ziming

Donate
======

如果本仓库对你有帮助，可以请作者喝杯速溶咖啡
