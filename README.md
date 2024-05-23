# techgig
from collections import defaultdict

def max_teams_with_same_weight(N, weights):
    # Count frequency of each weight
    weight_count = defaultdict(int)
    for weight in weights:
        weight_count[weight] += 1

    max_teams = 0

    # Check all possible sums from 2 to 2*N (since 1 ≤ Wi ≤ N)
    for s in range(2, 2 * N + 1):
        current_teams = 0
        temp_count = weight_count.copy()

        # Try to form pairs (a, b) such that a + b = s
        for weight in weights:
            if weight < s:
                other_weight = s - weight
                if temp_count[weight] > 0 and temp_count[other_weight] > 0:
                    if weight == other_weight and temp_count[weight] < 2:
                        continue
                    current_teams += 1
                    temp_count[weight] -= 1
                    temp_count[other_weight] -= 1

        max_teams = max(max_teams, current_teams)

    return max_teams

# Input reading
N = int(input())
weights = list(map(int, input().split()))

# Calculate the maximum number of teams
result = max_teams_with_same_weight(N, weights)
print(result)
