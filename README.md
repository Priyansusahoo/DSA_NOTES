# DSA_NOTES

## 3 Sum

  ```java
    class Solution {
    public List<List<Integer>> threeSum(int[] nums) {

            /**
             * Time-Complxeity : O(N^3)
             * Space-Complexity : O(k)
             */
    
            final int n = nums.length;
    
            Set<List<Integer>> set = new HashSet<>();
    
            for (int i = 0; i < n; i++) {
                for (int j = i + 1; j < n; j++) {
                    for (int k = j + 1; k < n; k++) {
                        if (nums[i] + nums[j] + nums[k] == 0) {
                            List<Integer> temp = new ArrayList<>(Arrays.asList(nums[i], nums[j], nums[k]));
    
                            Collections.sort(temp);
    
                            set.add(temp);
                        }
                    }
                }
            }
            return new ArrayList<>(set);
        }
    }
  ```
## Longest Substring Without Repeating Characters

  ```java
    class Solution {
    public int lengthOfLongestSubstring(String s) {
        final int n = s.length();

            /**
             * Time-Complexity : O(N^2)
             * Space-Complexity : O(256)
             */
            
            int max = Integer.MIN_VALUE;
    
            for (int i = 0; i < n; i++) {
                int[] hashArray = new int[256];
                int len = 0;
                for (int j = i; j < n; j++) {
                    int index = hash(s.charAt(j));
    
                    if (hashArray[index] == 1) {
                        break;                    
                    } else {
                        hashArray[index] = 1;
                        len = j - i + 1;
                        max = Math.max(max, len);
                    }
                }
            }
            return (max == Integer.MIN_VALUE) ? 0 : max;
        }
    /*
    abcabcbb
    */
        public static int hash(char c) {
            return c + 1;
        }
    }
  ```
## Group Anagrams
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> hm = new HashMap<>();

        for (String s : strs) {
            int[] count = new int[26];

            for (char c : s.toCharArray()) {
                count[ c - 'a']++;
            }

            StringBuilder sb = new StringBuilder();

            for (int i : count) {
                sb.append("#");
                sb.append(i);
            }

            String key = sb.toString();

            if (hm.containsKey(key)) {
                hm.get(key).add(s);
            } else {
                ArrayList<String> list = new ArrayList<>();
                list.add(s);
                hm.put(key, list);
            }
        }
        return new ArrayList(hm.values());
    }
}



// ------------------------------ BRUTE_FORCE----------------------------------
/**
 * NOTE:
 * This is a BRUTE-FORCE Approach and is NOT recommended as a valid solution
 *
 * **Understanding purpose only**
 *
 * Time-Complexity : O(n * k log k) // 's' --> length of 'strs' array & 'k' -> length of each string in strs[]
 *
 * Space-Complexity : O(n) // we are creating a Map
 */

// class Solution {

//     /**
//      * @param strs contains 'n' no. of strings
//      * @return a list of lists, where each list contains strings that are anagrams of each other
//      */
//     public List<List<String>> groupAnagrams(String[] strs) {
//         Map<String, List<String>> hm = new HashMap<>();

//         int n = strs.length;

//         for (int i = 0; i < n; i++) { // iterate over all the strings in []
//             String s = strs[i];

//             // sorting the String
//             char[] sArr = s.toCharArray();
//             Arrays.sort(sArr);
//             String sortedString = new String(sArr); // sorted String

//             // check if the sorted string exists or not
//             if (hm.containsKey(sortedString)) { // if exists we add the current element i.e 's' to the list
//                 hm.get(sortedString).add(s);
//             } else { // else we insert the sorted string and the current element i.e 's'
//                 List<String> newList = new ArrayList<>();
//                 newList.add(s);
//                 hm.put(sortedString, newList);
//             }
//         }

//         return returnValues(hm);
//     }

//     /**
//      * @param hashMap contains the sorted String as key and all the anagrams as list of string
//      * @return a list of lists, where each list contains strings that are anagrams of each other
//      *
//      * this method iterates over the Map values and returns the values as a List<List<String>> 
//      */
//     public static List<List<String>> returnValues(Map<String, List<String>> hashMap) {
//         List<List<String>> result = new ArrayList<>();

//         for (List<String> list : hashMap.values()) {
//             result.add(list);
//         }

//         return result;
//     }
// }
```

## Maximum Subarray
```java
class Solution {
    public int maxSubArray(int[] nums) {
        final int n = nums.length;

        int max = Integer.MIN_VALUE;

        /**
         * Time-Complexity ~ O(N^3)
         * Space-Complexity : O(1)
         */

        /*for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int sum = 0;
                for (int k = i; k <= j; k++) {
                    sum += nums[k];
                    max = Math.max(max, sum);
                }
            }
        }
        return max;*/

        /**
         * Time-Complexity : O(N^2)
         * Space-Complexity : O(1)
         */
        /*for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                max = Math.max(max, sum);
            }
        }
        return max;*/

        /**
         * Time-Complexity : O(N)
         * Space-Complexity : O(1)
         */
         
        int sum = 0;
        for (int i = 0; i < n; i++) {

            sum += nums[i];

            max = Math.max(max, sum);

            if (sum < 0) {
                sum = 0;
            }
        }
        return max;
    }
}


/*
5,4,-1,7,8


*/
```
## Product of Array Except Self
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        final int n = nums.length;

        /**
         * Time-Complexity : O(N^2)
         * Space-Complexity : O(N)
         */

        
        /*int[] newArray = new int[n];
        for (int i = 0; i < n; i++) {
            int product = 1;
            for (int j = 0; j < n; j++) {
                if (j != i) {
                    product *= nums[j];
                }
                newArray[i] = product;
            }
        }
        return newArray;*/

        // ---------------------------------------------------------

        /**
         * Time-Complexity : O(N)
         * Space-Complexity : O(N)
         */

        int[] left = new int[n];
        left[0] = 1;
        for(int i = 1; i < n; i++) {
            left[i] = left[i-1] * nums[i-1];
        }


        int[] right = new int[n];
        right[n-1] = 1;
        for(int i = n-2; i >= 0; i--) {
            right[i] = right[i+1] * nums[i+1];
        }


        int[] newArray = new int[n];
        for(int i = 0; i < n; i++) {
            newArray[i] = left[i] * right[i];
        }

        return newArray;



    }
}

/*
1,2,3,4

1,1,1*2,1*2*3
2*3*4*1,3*4*1,4*1,1

1,1,2,6
24,12,4,1


24,12,8,6
*/
```



## Reverse Linked List
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        
        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
}
```

