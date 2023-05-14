# 2106. 摘水果

## 自实现：前缀+二分查找

**注意lower_bound和upper_bound的实现**

- lower_bound：第一个大于等于target的索引
- upper_bound：第一个大于target的索引



**代码**:

```java
public class Main {

        // 查找第一个大于目标的下标
        public static int upper_bound(List<Integer> arr, int begin, int end, int tar) {
            while(begin < end) {
                int mid = begin + (end - begin) / 2;
                if(arr.get(mid) <= tar)
                    begin = mid + 1;
                else if(arr.get(mid) > tar)
                    end = mid;
            }
            return begin;
        }


        // 查找第一个大于等于的元素
        public static int lower_bound(List<Integer> arr, int begin, int end, int tar) {
            while(begin < end) {
                int mid = begin + (end - begin) / 2;
                // 当 mid 的元素小于 tar 时
                if(arr.get(mid) < tar)
                    // begin 为 mid + 1, arr[begin] 的值会小于或等于 tar
                    begin = mid + 1;
                    // 当 mid 的元素大于等于 tar 时
                else if(arr.get(mid) >= tar)
                    end = mid;
            }
            return begin;
        }


    public int maxTotalFruits(int[][] fruits, int startPos, int k) {
        int n = fruits.length;
        ArrayList<Integer> sum = new ArrayList<>();
        sum.add(0);
        for (int i = 1; i <= n; i++) {
            sum.add(fruits[i-1][1]+sum.get(i-1));
        }

        ArrayList<Integer> pos = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            pos.add(fruits[i][0]);
        }

        int ans = 0;
        for (int x = k; x >=0 ; x--) {
            int y = (k-x)/2;
            int l,r;
            l = startPos-x;
            r  = startPos+y;
            int pl = lower_bound(pos, 0, pos.size(), l);
            int pr = upper_bound(pos,0,pos.size(),r);
            ans = Math.max(ans,sum.get(pr)-sum.get(pl));

            l = startPos-y;
            r = startPos+x;
            pl = lower_bound(pos, 0, pos.size(), l);
            pr = upper_bound(pos,0,pos.size(),r);
            ans = Math.max(ans,sum.get(pr)-sum.get(pl));

        }
        return ans;

    }

    public static void main(String[] args) {

        int[][] fruits = {{2, 8}, {6, 3}, {8, 6}};
        int startPos = 5;
        int k =  4;

        System.out.println(new Main().maxTotalFruits(fruits,startPos,k));



    }
```



## 滑动窗口（双指针）

[摘水果 - 摘水果 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-fruits-harvested-after-at-most-k-steps/solution/zhai-shui-guo-by-leetcode-solution-4j9v/)





# 1419.数青蛙

本体重点：如何判断一个字符串是由某一个子串混合而成（通过计数）

```java
class Solution {
    public int minNumberOfFrogs(String croakOfFrogs) {
        if (croakOfFrogs.length() % 5 != 0) {
            return -1;
        }
        int res = 0, frogNum = 0;
        int[] cnt = new int[4];
        Map<Character, Integer> map = new HashMap<Character, Integer>() {{
            put('c', 0);
            put('r', 1);
            put('o', 2);
            put('a', 3);
            put('k', 4);
        }};
        for (int i = 0; i < croakOfFrogs.length(); i++) {
            char c = croakOfFrogs.charAt(i);
            int t = map.get(c);
            if (t == 0) {
                cnt[t]++;
                frogNum++;
                if (frogNum > res) {
                    res = frogNum;
                }
            } else {
                if (cnt[t - 1] == 0) {
                    return -1;
                }
                cnt[t - 1]--;
                if (t == 4) {
                    frogNum--;
                } else {
                    cnt[t]++;
                }
            }
        }
        if (frogNum > 0) {
            return -1;
        }
        return res;
    }
}
```

