👀 Number of Visible People in a Queue🧩 Problem StatementThere are n people standing in a queue, numbered from 0 to n - 1 from left to right. You are given an array heights of distinct integers, where heights[i] represents the height of the i-th person.👁️ Visibility RuleA person can see another person to their right if:i < j, andall people between them are shorter than both of them.Formally:min(heights[i], heights[j]) > max(heights[i+1] ... heights[j-1])📊 Visual ExplanationExample WalkthroughInput: heights = [10, 6, 8, 5, 11, 9]Output: [3, 1, 2, 1, 1, 0]Person 0 (Ht: 10): Sees heights 6, 8, and 11. The person with height 11 is taller than person 0 and blocks the view of anyone further right.Person 1 (Ht: 6): Sees only height 8.Person 2 (Ht: 8): Sees heights 5 and 11.Person 4 (Ht: 11): Sees height 9.🚀 Solution (Java)Javaimport java.util.*;

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
