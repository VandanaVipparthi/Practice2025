## Pattern 1: Sliding Window
The sliding window technique is used to efficiently process a contiguous section of data (like a substring or subarray) while avoiding unnecesary recomputation.
### 1. Find Averages of Sub Arrays
https://leetcode.com/problems/maximum-average-subarray-i/
````java
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
````
<b>Brute Force Approach</b>
This algorithm will find all the sum of k contiguous arrays and then find the average. 
Time Complexity: O(N*K)
Space Complexity: O(1)
````java
double findAvgOfSubArrays(int[] nums, int k){
  double ans=Double.MIN_VALUE;
        for(int i=0;i<nums.length-k+1;i++){
            double sum=0;
            for(int j=i;j<i+k;j++){
            sum+=nums[j];
            }
            ans=Math.max(ans,sum/k);
        }
        return ans;
}
````
Inneficiency: The inefficiency is that for any two consecutive subarrays of size `k`, the overlapping part (which will contain k-1 elements) will be evaluated twice.

<b> Optimized Approach </b>
In this approach first we will calculate the sum of first K elements and store the value. Then slide the window by one element while sliding add the rightmost element in window and remove the leftmost element in the array. 
````java

double findAvgOfSubArrays(int[] nums, int k){
  double sum=0;
  for(int i=0;i<k;i++){
    sum+=nums[i];
  }
  double maxSum =sum;
  for(int i=k; i<nums.length;i++){
    sum+=nums[i]-nums[i-k];
    maxSum=Math.max(maxSum,sum);
  }
  return maxSum/k;
}
````
Time Complexity: O(N)
Space Complexity: O(1)

### 2. Max Sum Subarray of size K
https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1
This algorithm will find all the sum of k contiguous arrays and then find the max. 
Time Complexity: O(N*K)
Space Complexity: O(1)
````java
public int maximumSumSubarray(int[] nums, int k) {
      // Code here
      int sum=0;
      for(int i=0;i<k;i++){
        sum+=nums[i];
      }
      int maxSum =sum;
      for(int i=k; i<nums.length;i++){
        sum+=nums[i]-nums[i-k];
        maxSum=Math.max(maxSum,sum);
      }
      return maxSum;
    }
````
Inneficiency: The inefficiency is that for any two consecutive subarrays of size `k`, the overlapping part (which will contain k-1 elements) will be evaluated twice.

<b> Optimized Approach </b>
In this approach first we will calculate the sum of first K elements and store the value. Then slide the window by one element while sliding add the rightmost element in window and remove the leftmost element in the array. 
````java

public int maximumSumSubarray(int[] nums, int k) {
  int sum=0;
  for(int i=0;i<k;i++){
    sum+=nums[i];
  }
  int maxSum =sum;
  for(int i=k; i<nums.length;i++){
    sum+=nums[i]-nums[i-k];
    maxSum=Math.max(maxSum,sum);
  }
  return maxSum;
}
````
Time Complexity: O(N)
Space Complexity: O(1)

### 3. Minimum Size Subarray Sum
https://leetcode.com/problems/minimum-size-subarray-sum/description/
````java
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
````
<b>Brute Force Approach</b>
````java
public int minSubArrayLen(int target, int[] nums) {
        int len=nums.length;
        boolean ans= false;
        for(int i=0;i<nums.length;i++){
            int sum=0;
            for(int j=i;j<nums.length;j++){
                sum+=nums[j];
                if(sum==target){
                    ans=true;
                    System.out.println(sum+" "+i+" "+j);
                    len=Math.min(len,j-i+1);
                }
            }
        }
        return ans?len:0;
    }
````
This algorithm will find all the sum of k contiguous arrays and then find the max. 
Time Complexity: O(N^2)
Space Complexity: O(1)

<b> Optimized Approach </b>
In this approach we iterate and calculate the sum, if sum > =target then we will change our window size by increasing the left pointer untill the sum>target and parallelly calculate the length of subarray.
````java
public int minSubArrayLen(int target, int[] nums) {
        int n=nums.length;
        int l=0,r=0;
        int sum=0;
        int ans=Integer.MAX_VALUE;
        while(r<n){
            sum+=nums[r];
            while(l<n && sum>=target){
                ans = Math.min(ans,r-l+1);
                sum -= nums[l];
                l++;
            }
            r++;
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 4. Longest Substring with K Uniques
https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1
````java
Input: s = "aabacbebebe", k = 3
Output: 7
Explanation: "cbebebe" is the longest substring with 3 distinct characters.
````
<b> Optimized Approach </b>
````java
public int longestkSubstr(String s, int k) {

        HashMap<Character, Integer> map = new HashMap<>();
        // l is left pointer of the window and r is the right pointer
        int l=0,r=0;
        int n=s.length();
        int mlen=-1;
        while(r<n){
            //put the data into map if there's no occurence it'll be 0 if its already present it'll increment the count of it.
            map.put(s.charAt(r),map.getOrDefault(s.charAt(r),0)+1);
            //if the map reached size k then calculate the length of the substring and store it
            if(map.size()==k){
                mlen=Math.max(mlen,r-l+1);
            }
            //if map size is > k that means we have to move our left pointer
            //We'll be moving left pointer till we reach a window of size <k so that we can move our right pointer for further substring
            else if(map.size()>k){
                while(l<n && map.size()>k){
                    int val=map.get(s.charAt(l));
                    val--;
                    if(val>0){
                        map.put(s.charAt(l),val);
                    }
                    else{
                        map.remove(s.charAt(l));
                    }
                    l++;
                }
            }
            r++;
        }
        return mlen;
        
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 5. Fruits into Baskets
https://leetcode.com/problems/fruit-into-baskets/

<b> Optimized Approach </b>
````java
Use a HashMap to count the frequency of each fruit in the current window.
Expand the window by moving the right pointer.
If the number of fruit types exceeds 2, shrink the window from the left until we’re back to 2 types.
Track the maximum window size during this process.
````
````java
public int totalFruit(int[] fruits) {      
        HashMap<Integer,Integer> map = new HashMap<>();
        int l=0,r=0,uniq=0,mlen=0,k=2;
        while(r<fruits.length){
            map.put(fruits[r],map.getOrDefault(fruits[r],0)+1);
            if(map.size()<=k){
                mlen=Math.max(mlen,r-l+1);
            }
            else if(map.size()>k && l<fruits.length){
                int val =map.get(fruits[l]);
                val--;
                if(val>0){
                    map.put(fruits[l],val);
                }
                else{
                    map.remove(fruits[l]);
                }
                l++;
            }
            r++;  
        }
        return mlen; 
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 6. Longest Substring with At Most Two Distinct Characters
https://www.naukri.com/code360/problems/longest-substring-with-at-most-two-distinct-characters_3125863?leftPanelTabValue=PROBLEM

<b> Optimized Approach </b>
````java
public static int lengthOfLongestSubstring(String s) {
		// Write your code here.
		HashMap<Character,Integer> map = new HashMap<>();
		int n=s.length();
		int l=0,r=0,mlen=0,k=2;
		while(r<n){
			map.put(s.charAt(r),map.getOrDefault(s.charAt(r),0)+1);
			if(map.size()<=k){
				mlen=Math.max(mlen, r-l+1);
			}
			else if(map.size()>k){
				while(map.size()>k && l<n){
					int val = map.get(s.charAt(l));
					val--;
					if(val>0){
						map.put(s.charAt(l),val);
					}
					else{
						map.remove(s.charAt(l));
					}
					l++;
				}
				
			}
			r++;
		}
		return mlen;
	}
 ````
Time Complexity: O(N)
Space Complexity: O(1)

### 7. No-repeat Substring
https://www.naukri.com/code360/problems/longest-substring-with-at-most-two-distinct-characters_3125863?leftPanelTabValue=PROBLEM

<b> Optimized Approach </b>
````java
Use two pointers: left and right
Use a HashSet to track characters in the current window
Expand right until you hit a duplicate
Then shrink left to remove duplicates
Track the maximum window size
````
````java
public int lengthOfLongestSubstring(String s) {
        HashMap<Character,Integer> map = new HashMap<>();
        int l=0,r=0,mlen=0,n=s.length();
        while(r<n && l<n){
            if(map.containsKey(s.charAt(r))){
                l=Math.max(l,map.get(s.charAt(r))+1);
            }
            map.put(s.charAt(r),r);
            mlen=Math.max(mlen,r-l+1);
            r++;
            
        }
        return mlen;
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 8.Longest Repeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement/description/
````java
Use the sliding window technique to expand and shrink a window in the string.
Maintain a frequency array to count characters in the window.
Find the character with the maximum frequency in the window.
If replacements needed = (window size - max frequency) > k, shrink from the left.
Track the maximum valid window length throughout the loop.
````
````java
public int characterReplacement(String s, int k) {
        HashMap<Character,Integer> map = new HashMap<>();
        int l=0,mlen=0,n=s.length(),mfreq=0;
        for(int r=0;r<n;r++){
            map.put(s.charAt(r),map.getOrDefault(s.charAt(r),0)+1);
            mfreq=Math.max(mfreq,map.get(s.charAt(r)));
            if((r-l+1)-mfreq>k){
                map.put(s.charAt(l),map.get(s.charAt(l))-1);
                l++;
            }
            mlen = Math.max(mlen, r - l + 1);
        }
        return mlen;
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 9. Max Consecutive Ones III
https://leetcode.com/problems/max-consecutive-ones-iii/description/
````java
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.
````
<b> Optimized Approach </b>
````java
public int longestOnes(int[] nums, int k) {
        int l=0,mlen=0,n=nums.length,zeros=0;
        for(int r=0; r<n; r++){
            if(nums[r]==0){
                zeros++;
            }
            while(zeros>k && l<n){
                if(nums[l]==0){
                    zeros--;
                }
                l++;
            }
            if(k>=0){
                mlen=Math.max(mlen,r-l+1);
            }
        }
        return mlen;
    }
````
Time Complexity: O(N)
Space Complexity: O(1)
### 10.  Permutation in String
https://leetcode.com/problems/permutation-in-string/description/

````java
Use a sliding window of size len(s1) over s2
Track the character frequency in both strings
Slide the window one step at a time, update counts, and compare
If any window matches the s1 count — we found a permutation!
````
<b> Optimized Approach </b>
````java
public boolean checkInclusion(String s1, String s2) {
        if(s1.length()>s2.length()){
            return false;
        }
        HashMap<Character,Integer> map1 = new HashMap<>();
        HashMap<Character,Integer> map2 = new HashMap<>();

        for(int i=0;i<s1.length();i++){
            map1.put(s1.charAt(i),map1.getOrDefault(s1.charAt(i),0)+1);
            map2.put(s2.charAt(i),map2.getOrDefault(s2.charAt(i),0)+1);
        }
        if(map1.equals(map2)){
            return true;
        }
        int left=0;
        for(int right=s1.length();right<s2.length();right++){
            map2.put(s2.charAt(right),map2.getOrDefault(s2.charAt(right),0)+1);
            map2.put(s2.charAt(left),map2.getOrDefault(s2.charAt(left),0)-1);
            if(map2.get(s2.charAt(left))<=0){
                map2.remove(s2.charAt(left));
            }
            left++;
            if(map1.equals(map2)){
            return true;}
        }
        return false;

    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 11. Find All Anagrams in a String
https://leetcode.com/problems/find-all-anagrams-in-a-string/solutions/
````java
Similar to the previous question
````
<b> Optimized Approach </b>
````java
public List<Integer> findAnagrams(String s2, String s1) {
        List<Integer> ans =new ArrayList<>();
        if(s1.length()>s2.length()){
            return ans;
        }
        HashMap<Character,Integer> map1 = new HashMap<>();
        HashMap<Character,Integer> map2 = new HashMap<>();

        for(int i=0;i<s1.length();i++){
            map1.put(s1.charAt(i),map1.getOrDefault(s1.charAt(i),0)+1);
            map2.put(s2.charAt(i),map2.getOrDefault(s2.charAt(i),0)+1);
        }
        if(map1.equals(map2)){
            ans.add(0);
        }
        int left=0;
        for(int right=s1.length();right<s2.length();right++){
            map2.put(s2.charAt(right),map2.getOrDefault(s2.charAt(right),0)+1);
            map2.put(s2.charAt(left),map2.getOrDefault(s2.charAt(left),0)-1);
            if(map2.get(s2.charAt(left))<=0){
                map2.remove(s2.charAt(left));
            }
            left++;
            if(map1.equals(map2)){
            ans.add(left);}
        }
        return ans;
    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 12. Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring/description/
````java
We will keep a running count of every matching instance of a character.
Whenever we have matched all the characters, we will try to shrink the window from the beginning, keeping track of the smallest substring that has all the matching characters.
We will stop the shrinking process as soon as we remove a matched character from the sliding window. One thing to note here is that we could have redundant matching characters, e.g., we might have two a in the sliding window when we only need one a. In that case, when we encounter the first a, we will simply shrink the window without decrementing the matched count. We will decrement the matched count when the second a goes out of the window.
````
<b> Optimized Approach </b>
````java
public String minWindow(String s, String t) {
        if(s==null || t==null || s.length()<t.length()){
            return new String();
        }
        HashMap<Character,Integer> map =new HashMap<>();
        int counter=0,l=0,r=0,sIndex=-1,minlen=Integer.MAX_VALUE;
        for(int i=0;i<t.length();i++){
            map.put(t.charAt(i),map.getOrDefault(t.charAt(i),0)+1);
        }
        while(r<s.length()){
            if(map.containsKey(s.charAt(r)) && map.get(s.charAt(r))>0){
                counter++;
            }
            map.put(s.charAt(r),map.getOrDefault(s.charAt(r),0)-1);
            while(counter==t.length() && l<s.length()){
                if(r-l+1<minlen){
                    minlen=r-l+1;
                    sIndex=l;
                }
                map.put(s.charAt(l),map.getOrDefault(s.charAt(l),0)+1);
                if(map.get(s.charAt(l))>0){
                    counter--;
                }
                l++;
            }
            r++;
        }
        return minlen==Integer.MAX_VALUE? new String(): new String(s.toCharArray(),sIndex,minlen);

    }
````
Time Complexity: O(N)
Space Complexity: O(1)

### 13. Substring with Concatenation of All Words
https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/
````java
Fixed Sliding Window Size
.Each valid substring must have a length of total_length = words.length * word_length.
.We slide a window of this size across s.

Use a Hash Map to Store Word Frequencies
.Store word counts in wordMap.
.Extract substring chunks of size word_length from s and compare against wordMap using a second hash map.

Sliding Window with Multiple Start Points
.Since words are of fixed length, we try sliding from 0 to word_length - 1.
````
<b> Optimized Approach </b>
````java
public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new ArrayList<>();
        if (s == null || s.length() == 0 || words == null || words.length == 0) return result;

        int wordLength = words[0].length();
        int numWords = words.length;
        int totalLength = wordLength * numWords;

        
        Map<String, Integer> wordMap = new HashMap<>();
        for (String word : words) {
            wordMap.put(word, wordMap.getOrDefault(word, 0) + 1);
        }

        
        for (int i = 0; i < wordLength; i++) {
            int left = i, right = i;
            int count = 0; 
            Map<String, Integer> windowMap = new HashMap<>();
            while (right + wordLength <= s.length()) {
                String word = s.substring(right, right + wordLength);
                right += wordLength;

                if (wordMap.containsKey(word)) {
                    windowMap.put(word, windowMap.getOrDefault(word, 0) + 1);
                    count++;  
                    while (windowMap.get(word) > wordMap.get(word)) {
                        String leftWord = s.substring(left, left + wordLength);
                        left += wordLength;
                        windowMap.put(leftWord, windowMap.get(leftWord) - 1);
                        count--;
                    }
                    if (count == numWords) {
                        result.add(left);
                    }
                } else {
                    
                    windowMap.clear();
                    count = 0;
                    left = right;
                }
            }
        }

        return result;
    }
````
Time complexity:O(N×W)

Space complexity:O(W)
