# 滑动窗口

一般针对数组和字符串



## 159.至多包含两个不同字符的最长子串

哈希计数+滑动窗口

```java
public int lengthOfLongestSubstringTwoDistinct(String s) {
        if (s.isEmpty()) return 0;
        HashMap<Character, Integer> map = new HashMap<>();
        char[] chars = s.toCharArray();
        int n = chars.length;
        int slow = 0;
        int fast = 0;
        int res = 0;
        while (fast<=n-1) {
            char item = chars[fast];
            map.put(item,map.getOrDefault(item,0)+1);
            if (map.keySet().size()<=2) {
               fast++;
           }else {
                while (map.keySet().size()>2){
                    char items = chars[slow];
                    map.put(items,map.get(items)-1);
                    if (map.get(items)==0) map.remove(items);
                    slow++;
                }
                fast++;
           }

           res = Math.max(res,1+fast-slow);

        }
        return res-1;
    }
```

