import java.util.*;



class Solution {
    public int[] canSeePersonsCount(int[] arr) {
        int n = arr.length;
        int[] ans = new int[n];
        Stack<Integer> st = new Stack<>();
        
        // Initialize with the last person
        st.push(arr[n - 1]);
        ans[n - 1] = 0;

        for (int i = n - 2; i >= 0; i--) {
            int count = 0;

            // Count all shorter people to the right (they are visible)
            while (st.size() > 0 && st.peek() <= arr[i]) {
                count++;
                st.pop();
            }

            // VERY VERY IMPORTANT: If stack size > 0, we found the next greater element.
            // This person is visible but blocks the view of anyone behind them.
            if (st.size() > 0) {
                count++;
            }

            ans[i] = count;
            st.push(arr[i]);
        }
        return ans;
    }
}
