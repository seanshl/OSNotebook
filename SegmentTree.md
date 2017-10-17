### 线段树

1. **原理**

2. **适用范围**

3. **相关题目**
	* __307 Range Sum Query - Mutable__
		1. 题目: Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive. The update(i, val) function modifies nums by updating the element at index i to val.
		2. 例子: 
			* ```
				Given nums = [1, 3, 5]

				sumRange(0, 2) -> 9
				update(1, 2)
				sumRange(0, 2) -> 8
			  ```
		3. 解法
		* ```
			public class NumArray {
				private class SegmentTreeNode {
					int val;
					int start, end;
					SegmentTreeNode left, right;
					public SegmentTreeNode(int start, int end) {
						this.val = 0;
						this.start = start;
						this.end = end;
					}
				}

				private SegmentTreeNode root;

				private SegmentTreeNode buildTree(int[] nums, int start, int end) {
					if (start > end) {
						return null;
					}

					SegmentTreeNode node = new SegmentTreeNode(start, end);
					if (start == end) {
						node.val = nums[start];
					} else {
						int mid = start + (end - start) / 2;
						node.left = buildTree(nums, start, mid);
						node.right = buildTree(nums, mid + 1, end);
						node.val = node.left.val + node.right.val;
					}

					return node;
				}

				private void update(SegmentTreeNode node, int pos, int val) {
					if (node.start == node.end) {
						node.val = val;
					} else {
						int mid = node.start + (node.end - node.start) / 2;
						if (pos <= mid) update(node.left, pos, val);
						else update(node.right, pos, val);

						node.val = node.left.val + node.right.val;
					}
				}

				public NumArray(int[] nums) {
					this.root = buildTree(nums, 0, nums.length - 1);
				}

				public void update(int i, int val) {
					this.update(root, i, val);
				}

				public int sumRange(int i, int j) {
					return sumRange(root, i, j);
				}

				private int sumRange(SegmentTreeNode node, int start, int end) {
					if (node.end == end && node.start == start) return node.val;

					int mid = node.start + (node.end - node.start) / 2;
					if (end <= mid) return sumRange(node.left, start, end);
					else if (start >= mid + 1) return sumRange(node.right, start, end);
					else {
						return sumRange(node.left, start, mid) + sumRange(node.right, mid + 1, end);
					}
				}
			}
			
		```
