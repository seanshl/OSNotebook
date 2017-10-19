
0. [Summary](https://discuss.leetcode.com/topic/50315/a-summary-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently/2)

1. Operations

	

2. 用 亦或^ 来移除偶数个相同的数组并且留下奇数
	

3. 例题
	1. 计算一个整数的bit位为1的个数
		*   ```
				public class Solution {
					// you need to treat n as an unsigned value
					public int hammingWeight(int n) {
						int count = 0;
						while (n != 0) {
							n = n & (n - 1);
							count++;
						}
						return count;
					}
				}
			 ```
	2. 判断是否是2的次幂
		*    ```
			    public boolean isPowerOfTwo(int n) {
					if (n <= 0) return false;
					return (n & (n - 1)) == 0;
				}
			 ```
	 3. sum of two integers.
	 	* 	```
			    public int getSum(int a, int b) {
					if (a == 0) return b;
					else if (b == 0) return a;

					while (b != 0) {
						int carry = a & b;
						a = a ^ b;
						b = carry << 1;
					}

					return a;
				}
			
			```
	4. reverse bits
		* 	```
			    public int reverseBits(int n) {
				int mask = 0;

				for (int i = 0; i < 32; i++) {
				    mask <<= 1;
				    if ((n & 1) == 1) mask++;
				    n >>= 1;
				}

				return mask;
			    }			
    			```
