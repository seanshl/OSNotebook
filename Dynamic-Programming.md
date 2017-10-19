
### 动态规划
1. **文章**
	* [leetcode总结无止境系列之动态规划及比较](http://cuijing.org/2013/07/summary-of-dynamic-programming-in-leetcode/)
	* [算法导论读书笔记之第15章 动态规划[总结]](http://www.cnblogs.com/Anker/archive/2013/03/15/2961725.html)
	* [通过金矿模型介绍动态规划](http://blog.csdn.net/woshioosm/article/details/7438834)
2. **基本思想**
	1. 通过__组合子问题__的解而解决整个问题，通过将问题分解为相互__不独立__(各个子问题包含有公共的子问题)的子问题，对每个子问题求解一次，将结果保存的哦啊一个辅助表中，避免每次遇到各个子问题时重新计算
	2. 通常用于解决__最优化问题__，核心的四个性质， **最优子问题，子问题重叠， 边界，子问题独立**.
	3. 子问题： 为了解决自己的问题，需要给别人制造另外的问题，但是另外的问题的结果可以很容易推导出自己的问题的结果
	4. **最优子结构**: 子问题最优化时，母问题通过优化选择后一定最优的情况叫做最优子结构
	5. **子问题重叠**: 用金矿模型中的例子：王也好，大臣也好，所有人面对的都是同样的问题，即给你一定数量的人，给你一定数量的金矿，让你求出能够开采出来的最多金子数。我们把这种母问题与子问题本质上是同一个问题的情况称为“子问题重叠”。然而问题中出现的不同点往往就是被子问题之间传递的参数，比如这里的人数和金矿数。
	6. **边界**：子问题在一定时候就不再需要提出子子问题的情况叫做边界，没有边界就会出现死循环。
	7. **子问题独立**: 一个母问题在对子问题选择时，当前被选择的子问题两两互不影响的情况叫做“子问题独立”。
	8. **做备忘录**: 问题的答案在一个变量中，如果再次遇到这个问题就直接从变量中获得答案，因此每一个问题仅会计算一遍，如果不做备忘的话，动态规划就没有任何优势可言了。             
	9. **时间复杂度分析**: O(questionCount * chooseCount)
	
3. **设计步骤**
	* 设计思路1
		1. 构造问题所对应的过程
		2. 思考过程的最后一个步骤，看看有哪些选择情况
		3. 找到最后一步的子问题，确保符合子问题重叠，把子问题中不相同的地方设置为参数
		4. 使得子问题符合最优子结构
		5. 找到边界，考虑边界的各种处理方式
		6. 确保满足子问题独立
		7. 考虑如何做备忘录
		8. 分析所需时间是否满足要求
		9. 写出转移方程式

4. 三板斧
	* 判断dp维数，帮助寻找递推公式
	* 写递推公式并查看边界条件, 举例子，画图表，类似数学归纳法
	* 降维打击： 减少空间复杂度(滚动数组)
	
5. **经典类型**
	* 金矿模型
		* 题述: 有一个包和n个物品，包的容量为m，每个物品都有各自的体积和价值，问当从这n个物品中选择多个物品放在包里而物品体积总数不超过包的容量m时，能够得到的最大价值是多少？[对于每个物品不可以取多次，最多只能取一次，之所以叫做01背包，0表示不取，1表示取]
		* 分析:
			* 为什么可以用动态规划？
				1. 解决最优化问题
				2. 
			
6. **例题**
	* 300 Longest Increasing Subsequence
		* 题述: 
			```
				Given an unsorted array of integers, find the length of longest increasing subsequence.

				For example,
				Given [10, 9, 2, 5, 3, 7, 101, 18],
				The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.
				Your algorithm should run in O(n2) complexity.
				Follow up: Could you improve it to O(n log n) time complexity?
			```
		* 解答:
		
			1. 解法1：DP 复杂度O(n^2)
				```
				class Solution {
				    public int lengthOfLIS(int[] nums) {
					if (nums.length < 2) return nums.length;

					int n = nums.length;
					int[] dp = new int[n];
					Arrays.fill(dp, 1);
					int max = 1;

					for (int i = 1; i < n; i++) {
					    for (int j = 0; j < i; j++) {
						if (nums[i] > nums[j]) {
						    dp[i] = Math.max(dp[j] + 1, dp[i]);
						}
					    }
					    max = Math.max(max, dp[i]);
					}

					return max;
				    }
				}
				```
			2. 解法2: DP
			```
			public class Solution {
			    public int lengthOfLIS(int[] nums) {
				int[] dp = new int[nums.length];
				int length = 0;

				for (int num : nums) {
				    //在dp的范围内去找到当前num应该插入的位置
				    int index = Arrays.binarySearch(dp, 0, length, num);

				    //当找不到时， binarysearch返回的是 - insert place - 1， 返回的依然是num应该插入的位置
				    if (index < 0) {
					index = - (index + 1);
				    }

				    //由于限制了bs的范围， 所以index最高也就是当前length + 1的位置。
				    //如果index != length, 直接更新现有dp中的某个值，否则扩展dp的实际长度
				    dp[index] = num;
				    if (index == length) {
					length++;
				    }
				}

				return length;
			    }
			}
		```
			
