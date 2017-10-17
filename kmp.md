
### 字符串匹配 KMP
1. __算法基础__
	* [阮一峰链接](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html)
	* [彻头彻尾理解kmp](http://blog.csdn.net/v_july_v/article/details/7041827)
2. __算法流程__
	1. __匹配流程__
		假设现在文本串S匹配到 i 位置，模式串P匹配到 j 位置
		* 如果j = -1，或者当前字符匹配成功（即S[i] == P[j]），都令i++，j++，继续匹配下一个字符；
		* 如果j != -1，且当前字符匹配失败（即S[i] != P[j]），则令 i 不变，j = next[j]。此举意味着失配时，模式串P相对于文本串S向右移动了j - next [j] 位。换言之，当匹配失败时，模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值（next 数组的求解会在下文的3.3.3节中详细阐述），即移动的实际位数为：j - next[j]，且此值大于等于1。

3. 例题
	* __Implement strStr()__
		```
		public class Solution {
			public int strStr(String haystack, String needle) {
				int[] kmp = buildKMP(needle);

				int i, j;
				for (i = 0, j = 0; i < haystack.length() && j < needle.length(); i++) {
					while (j > 0 && haystack.charAt(i) != needle.charAt(j)) {
						j = kmp[j - 1];
					}

					if (needle.charAt(j) == haystack.charAt(i)) {
						j++;
					}
				}

				return j == needle.length()? i - j : -1;
			}

			private int[] buildKMP(String needle) {
				int[] kmp = new int[needle.length()];

				int j = 0;
				for (int i = 1; i < needle.length(); i++) {
					while (j > 0 && needle.charAt(i) != needle.charAt(j)) {
						j = kmp[j - 1];
					}

					if (needle.charAt(j) == needle.charAt(i)) {
						j++;
					}

					kmp[i] = j;
				}

				return kmp;
			}
		}		
		```
