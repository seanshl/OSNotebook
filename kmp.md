
### 字符串匹配 KMP
1. __算法基础__
	* [阮一峰链接](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html)
	* [彻头彻尾理解kmp](http://blog.csdn.net/v_july_v/article/details/7041827)
	
2. 例题
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
