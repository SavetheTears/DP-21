# 198 - House Robber I
Conventional stuff, store the best outcome in the i-th place in a vector.
				             
# 213 - House Robber II
this time you are to rob houses aligned as a circle

head and end are connected. Only difference is to pick the first one or not. 

Consider using two integer variables to store contemporary values instead of two `nums.size()-1` vectors to save memory space

# 740 - delete and earn
Delete a number to get that number of points, but any numbers that are 1 less or more thant the number are automatically dropped and no points earned.

Intuitively, by deleting a number `n`, we need to go over the whole array to look for all `n-1`,`n`, `n+1`, that would take `O(n)` each time. Worst case would be O(n^2), If you do this, it is too expensive.

One useful trick is to consider a one-one bijection of the total score each number youcan get by deleting them. Maintain a vector where `vector[i]` is the number of `n` multiplied by n.

Then, we can see the similarity between this question and House Robber II problems. Take `n`, `n-1` and `n+1` cannot be taken. Neighbor problem.

Actually, we can see this trick in a lot of quick solutions using the input number limitation.

Notable quick solutions( 0ms):

	class Solution {
	public:
			int deleteAndEarn(vector<int>& nums) {
					// Get the max elt
					int m = *max_element(nums.begin(), nums.end());
					int n=nums.size();
					if (n==1)   return nums[0];
					// Create a s for values s with default 0 | and a vector for DP
					vector<int> s(m+1,0), dp(m+1,0);
					// Adjust s content
					for(int i=0; i<n;i++){
							s[nums[i]]++;
					}
					dp[0]=0; dp[1]=s[1];
					for(int i=2; i<=m;i++){
							// Max of taking the current value x times Vs keeping the value before (Since we're removing "n-1" & "n+1")
							dp[i]=max(dp[i-1], dp[i-2]+s[i]*i);
					}
					return dp[m];
			}
	};


that \*max_element function seems new feature in new C++ version? Needs looking into.
`s` tracks the \# of appearances of a number. `dp` is simply the array to track sums. Logic is the same... Why this one is much faster...
