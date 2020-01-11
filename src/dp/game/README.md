# 博弈论DP

- 掌握这种从后往前，dp记录差值、或者胜负（递推公式-dp）的思想


## 巴什博弈
两个顶尖聪明的人在玩游戏，有一堆nn个石子，每次每个人能取[1,m]个石子，不能拿的人输，请问先手与后手谁必败？

我们分类讨论一下这个问题：

当n≤m时，这时先手的人可以一次取走所有的；

当n=m+1时，这时先手无论取走多少个，后手的人都能取走剩下所有的；

当n=k∗(m+1)时，对于每m+1m+1个石子，先手取ii个，后手一定能将剩下的(m+1−i)(m+1−i)个都取走，因此后手必胜；

当n=k∗(m+1)+x(0 < x < m+1)时，先手可以先取xx个，之后的局势就回到了上一种情况，无论后手取多少个，先手都能取走m+1个中剩下的，因此先手必胜。

结论：
通过上面的分析可以得出结论：当n能整除m+1时先手必败，否则先手必胜。

## Nim博弈

两个顶尖聪明的人在玩游戏，有n堆石子，第i堆有ai个，每人每次能从一堆石子中取任意多个石子但不能不取，不能拿的人输，请问先手与后手谁必胜？

我们从简单的情况入手：

当n=1时，显然先手取走这一堆就能获胜；

当n=2且a1!=a2时，我们假设a1>a2，先手可以先在第一堆取走a1−a2个，下一次无论后手取走多少个，先手都可以在另一堆取走同样多个，因此先手必胜；

当n=2且a1==a2时，先手无论取走多少个，后手都能在另一堆取走同样多个，因此后手必胜。

当3≤n时呢？

问题变得繁琐起来，这时就要一个有规律性的结论。

结论：
当`a1^a2^…………^an=0`时先手必败，反之先手必胜。

为什么这个结论是对的？

假设当前异或和为0，这时先手在某一堆取走了若干个，局势变成了`a1^a2^…………^a′i^…………^an=k`，也就是`a1^a2^…………^a′i^…………an^k=0`。

假设k的最高位1在第x位，那么一定有一个数aj, aj的第xx位为1。

那么我们只要能将aj变成aj^k，就能使异或和又等于0，后手一直这样取，最后一定会是`a1=a2=……=an=0`（此处最重要），异或和是0，这时先手无法取了，先手就一定必败了。

那么能否每次都将aj变成aj^k呢 ?

答案是可以的，因为aj比k多出的高位异或后不变,第x位异或后为0,无论低位是什么，在第x位变0后整个数都会变小。

也就是说aj^k一定小于aj，那么后手每次只要在第j堆取走`aj−(aj^k)`个石子就好了。