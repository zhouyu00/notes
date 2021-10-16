# LeetCode239滑动窗口最大值
给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。返回滑动窗口中的最大值。

示例

输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3

输出: [3,3,5,5,6,7]

解释:
滑动窗口的位置 	最大值
[1 3 -1] -3 5 3 6 7 	3
1 [3 -1 -3] 5 3 6 7 	3
1 3 [-1 -3 5] 3 6 7 	5
1 3 -1 [-3 5 3] 6 7 	5
1 3 -1 -3 [5 3 6] 7 	6
1 3 -1 -3 5 [3 6 7] 	7

分析：

    很重要的一点，首先队首和队尾的下标差<=k
    如果在满足1的情况下，进来一个大于前面k-1个数的数字，则前面k-1个数字失去作用，同时也就失去保存的必要性，因此可以使用双端队列，这样可以保证窗口最大值始终在队列的最前面，为了保证条件1，因此选择存index

```java
class Main{
    public static int[] maxSlidingWindow(int[] nums, int k) {
        LinkedList<Integer> deque = new LinkedList<>();
        int[] res = new int[nums.length-k+1];
        for(int i=0;i<nums.length;i++){
            int t = nums[i];
            if(!deque.isEmpty()){
                int first = deque.peekFirst();
                while(!deque.isEmpty()&&(i-first>=k||nums[first]<=t)){
                    first = deque.pollFirst();
                }
            }
            deque.offerLast(i);
            if(i>=k-1){
                res[i-k+1]=nums[deque.peekFirst()];
            }
        }
        return res;
    }
    public static void main(String[] args) {
        int[] nums={1,3,-1,-3,5,3,6,7};
        int k = 3;
        int[] res =maxSlidingWindow(nums,k);
        PrintHelper.printArray(res);
    }
}
```
