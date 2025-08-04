# Competitive-Coding-6

Please submit the interview problems posted in slack channel here. The problems and statements are intentionally not shown here so that students are not able to see them in advance 
//Problem-1 (Beautiful Arrangements)
// Time Complexity : O(n!)
// Space Complexity : O(1)
// Did this code successfully run on Leetcode : yes
// Any problem you faced while coding this : no


// Your code here along with comments explaining your approach
1. In the backtrack function we will try to make different arrangements of the array and check if the action (arr[i] % ind == 0 || ind % arr[i] == 0)
    is valid? if yes then we will make new arrangements and call the backtrack function for ind+1 and check the same action 
2. If we reach the end of the array we will increase the count and return
3. We will now swap back the elements to their original position
class Solution {
    int count = 0;
    public int countArrangement(int n) {
        int[] arr = new int[n + 1]; 
        for (int i = 1; i <= n; i++){
            arr[i] = i;
        }

        backtrack(arr, 1, n);
        return count;
    }

    private void backtrack(int[] arr, int ind, int n) {
        if (ind > n) {
            count++;
            return;
        }

        for (int i = ind; i <= n; i++) {
            if (arr[i] % ind == 0 || ind % arr[i] == 0) {
                swap(arr, i, ind);
                backtrack(arr, ind + 1, n);
                swap(arr, i, ind);
            }
        }
    }

    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}


//Problem-2 (Logger Rate Limiter)
// Time Complexity : O(1)
// Space Complexity : O(m) m = unique messages
// Did this code successfully run on Leetcode : yes 
// Any problem you faced while coding this : no


// Your code here along with comments explaining your approach
1. We will have a hashmap that will store message as the key and their timestamp as the value
2. We will check if the message exists and if yes then we will check if the previous timestamp + 10 is less than current timestamp, if not return false
3. We will update our hashmap with the current timestamp and message and return true

class Logger {
    HashMap<String, Integer> log;

    public Logger() {
        log = new HashMap<>();
    }
    
    public boolean shouldPrintMessage(int timestamp, String message) {
        if(log.containsKey(message)){
            int value = log.get(message);

            if(value + 10 > timestamp){
                return false;
            }
            
        }
        log.put(message, timestamp);
        return true;
    }
}

/**
 * Your Logger object will be instantiated and called as such:
 * Logger obj = new Logger();
 * boolean param_1 = obj.shouldPrintMessage(timestamp,message);
 */
