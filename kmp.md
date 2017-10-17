
### 字符串匹配 KMP
1. __算法基础__
	* [阮一峰链接](http://www.ruanyifeng.com/blog/2013/05/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm.html)
	* [彻头彻尾理解kmp](http://blog.csdn.net/v_july_v/article/details/7041827)
2. __算法流程__
	1. __匹配流程__
		假设现在文本串S匹配到 i 位置，模式串P匹配到 j 位置
		* 如果j = -1，或者当前字符匹配成功（即S[i] == P[j]），都令i++，j++，继续匹配下一个字符；
		* 如果j != -1，且当前字符匹配失败（即S[i] != P[j]），则令 i 不变，j = next[j]。此举意味着失配时，模式串P相对于文本串S向右移动了j - next [j] 位。换言之，当匹配失败时，模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值（next 数组的求解会在下文的3.3.3节中详细阐述），即移动的实际位数为：j - next[j]，且此值大于等于1。
	2. __next数组__
		* next 数组各值的含义(长度与模式串相同)：代表当前字符之前的模式串中，有多大长度的相同前缀后缀。例如如果next [j] = k，代表j 之前的字符串中有最大长度为k 的相同前缀后缀。此也意味着在某个字符失配时，该字符对应的next 值会告诉你下一步匹配中，模式串应该跳到哪个位置（跳到next [j] 的位置）。如果next [j] 等于0或-1，则跳到模式串的开头字符，若next [j] = k 且 k > 0，代表下次匹配跳到j 之前的某个字符，而不是跳到开头，且具体跳过了k 个字符。
		* next 数组考虑的是除当前字符外的最长相同前缀后缀
	3. __匹配部分C++代码__
		```
		int KmpSearch(char* s, char* p)  
		{  
			int i = 0;  
			int j = 0;  
			int sLen = strlen(s);  
			int pLen = strlen(p);  
			while (i < sLen && j < pLen)  
			{  
				//①如果j = -1，或者当前字符匹配成功（即S[i] == P[j]），都令i++，j++      
				if (j == -1 || s[i] == p[j])  
				{  
					i++;  
					j++;  
				}  
				else  
				{  
					//②如果j != -1，且当前字符匹配失败（即S[i] != P[j]），则令 i 不变，j = next[j]      
					//next[j]即为j所对应的next值        
					j = next[j];  
				}  
			}  
			if (j == pLen)  
				return i - j;  
			else  
				return -1;  
		}  
		```
	4. __最大长度匹配表__
		
3. __算法时间复杂度__
	* O(m + n)
	* 优点在于能够避免让文本串的下标i回溯，i永远往前走，一步不回头
	
4. 例题
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
	* 459 Repeated Substring
		```
		public class Solution {
			public boolean repeatedSubstringPattern(String s) {
				if (s.isEmpty()) return false;
				int[] kmp = this.buildKMP(s);
				int n = s.length();

				int prefixLength = kmp[n - 1];
				int repeatLength = n - prefixLength;

				return prefixLength > 0 && n % repeatLength == 0;
			}

			private int[] buildKMP(String s) {
				int n = s.length();
				int[] kmp = new int[n];
				int j = 0;
				for (int i = 1; i < n; i++) {
					while (j > 0 && s.charAt(i) != s.charAt(j)) j = kmp[j - 1];
					if (s.charAt(i) == s.charAt(j)) j++;
					kmp[i] = j;
				}

				return kmp;
			}
		}
		```
		
	* Shortest Palindrome
	
	* Repeated String Match
	
	* Minimum Window Substring
	
	* Wildcard Matching
	
	* Add Bold Tag in String
