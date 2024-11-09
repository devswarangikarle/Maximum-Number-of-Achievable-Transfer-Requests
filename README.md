# Maximum-Number-of-Achievable-Transfer-Requests

We have n buildings numbered from 0 to n - 1. Each building has a number of employees. It's transfer season, and some employees want to change the building they reside in.

You are given an array requests where requests[i] = [fromi, toi] represents an employee's request to transfer from building fromi to building toi.

All buildings are full, so a list of requests is achievable only if for each building, the net change in employee transfers is zero. This means the number of employees leaving is equal to the number of employees moving in. For example if n = 3 and two employees are leaving building 0, one is leaving building 1, and one is leaving building 2, there should be two employees moving to building 0, one employee moving to building 1, and one employee moving to building 2.

Return the maximum number of achievable requests.

class Solution:
    def maximumRequests(self, n: int, requests: List[List[int]]) -> int:
        answer = 0
        indegree = [0 for _ in range(n)]

        def maxRequest(index, count):
            if(index == len(requests)):
                for i in range(n):
                    if(indegree[i]):
                        return
                nonlocal answer
                answer = max(answer, count)
                return

            indegree[requests[index][0]] -= 1
            indegree[requests[index][1]] += 1

            maxRequest(index + 1, count + 1)

            indegree[requests[index][0]] += 1
            indegree[requests[index][1]] -= 1

            maxRequest(index + 1, count)

        maxRequest(0, 0)

        return answer
