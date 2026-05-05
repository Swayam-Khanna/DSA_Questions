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
🧠 IntuitionMonotonic Stack: We process the array from right to left to maintain a stack of people whose visibility we are currently evaluating.Linear Efficiency: Since each person is pushed onto and popped from the stack exactly once, the time complexity remains $O(n)$.Space Complexity: $O(n)$ to store the stack.📌 TagsMonotonic Stack | Arrays | Stack | Greedy✍️ AuthorSwayam KhannaThird-year B.Tech in Computer Science and EngineeringChitkara University
