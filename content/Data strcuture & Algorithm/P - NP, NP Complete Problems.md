---
aliases:
  - NP 문제
  - P 대 NP
---
# 개요
> **N**ondeterministic **p**olynomial time **problems**

Ubiquitous intractability 가 있다. 많은 중요한 문제들이 효율적으로 풀리지 않는다.


## 문제들의 클래스와 tractability
효율적이라는 건 polynomial time 안에 풀 수 있다는 뜻이다.

**P-problem** : 다항시간 내에 풀 수 있는 문제들의 집합
- 곱셈
- 정렬

P-problem 이 아닌 문제들.
- (negative cycle 이 있을 때) 최단거리 구하기
- 배낭문제 (NP-hard)
- Traveling saleman problem
- 3SAT problem

**NP-problem** : **Nondeterministic Turing machine** 으로 다항시간 내에 풀 수 있는 문제들의 집합
- Subset sum problem
**다음 액션**이 여러가지가 가능한 경우. 라고 생각해도 좋다. 반대로 어느 액션을 취해야 할 지 중간에 알 수 없는 경우이기도 하다. 

**NP-hard** : 검산도 다항시간에 할 수 없다.

또 다른 클래스의 문제들도 있다.
- 중단 문제 (Halting problem)
이 클래스의 문제는 유한시간내에 풀 수 있을지 장담도 못한다. (배낭문제 등은 Brute-force 로 유한시간 내에 풀림)


## Reduction
Reduction : 귀결 정도로 번역할 수 도 있겠다.
- Median problem reduced to sorting problem.
- All-pair shortest path reduced to single source shortest path problem.
- **Large problem reduced to small subroutine.**

> [!NOTE] NP Completeness
>문제 1 이 문제 2 로 reduce 될 때, 문제 1 이 P-problem 이 아니면 문제 2 도 그렇다. 
>어떤 집합과 연산에 대해 complete 하다는 건, 각 집합의 원소들에 연산을 가해도 여전히 집합에 속한다는 것임.
>NP 문제 하나가 쉽게 풀리면 다른 모든 NP 문제도 쉽게 풀린다. (reduce 되기 때문)


결국 효율적으로 풀 수 없는 문제가 있다는건데, 이걸 알아서 뭐가 좋을까?
- 직면한 문제가 NP 인지 증명할 수 있으면 excuse 를 얻을 수 있다.
- 그러면 이제 **문제를 바꿀 수 있는 권한** 같은 걸 얻은 것이다. (이대로는 안풀리는 문제니까)
- Structured input 을 받거나, 제한 같은걸 둬서 P-problem 으로 최대한 바꾼다. (ex. 3SAT -> 2SAT)
- 혹은 Heuristic 을 사용한다 (guarantee 를 조금 포기한다 - compromise with correctness)
- 어쩔 수 없이 Exponential time 으로 풀지만, 최대한 최적화 한다. (brute-force 보단 낫게 설계)


# Some Best Solutions for NP-problem
Heuristic approach
Optimized but exponential

항상 sub-problem 을 고민해보자.

- Vertex Cover problem
undirected graph 에서 엣지를 모두 커버하는 vertex 를 고른다. 가장 적은 vertex 를 고르는 방법을 계산.
Tree 구조에선 P-problem 이다. (유명한 DP problem.)
Bipartite graph 구조에서도 효율적으로 풀린다. (이분 그래프)

커버할 Vertex 갯수를 정한 경우, $O(2^{k}n)$ 의 복잡도를 가진다. 이런 류의 문제를 Fixed Parameter Tractable (FPT) problem 이라고 한다. 커버 사이즈 k 가 정해져 있으면 선형 시간내에 (커버링 방법을) 구할 수 있다...

k 개로 커버할 수 있으면 <-> 한 엣지를 고르고 잇는 정점 둘 중 하나를 없앤, 두 경우중 최소 한 그래프에서, k-1 개로 커버가 된다.

이를 이용하면 1~2 번의 recursive call 을 하면서 풀 수 있다. (k-1 개의 정점을 제거했을 때 star + isolate 그래프가 되는 경우가 있으면 커버가 됨.)


# 유명한 NP 문제들

## Traveling Salesman problem
Brute-force search 로는 $O(n!)$ 이 걸린다. n = 12, 13 정도가 한계임. (1억~ 10억)

DP 를 사용하면 $O(n^{2}2^{n})$ 이 걸린다. 팩토리얼 보단 낫다. n = 30 정도도 커버 가능하다.

개인적인 감상이지만, DP 로 풀 때 항상 캐시가 제대로 구현된건지 체크해봐야 한다 (n  이 적당히 작을 때 캐시 기능을 껏다 켰다 하면서 같은 값이 나오는지 체크) 이 부분 체크 안해서 꽤 고생했다. (2024-07-13)


## Knapsack problem
유명한 NP 문제. 스케쥴링 문제처럼 ratio 를 이용해 greedy 로 푸는 heuristic 이 있다. (최적 솔루션의 50% 이상은 보장함.)

그 외에도 integer 로 값이 주어질 때 polynomial time complexity 가 나오기도 한다. (값의 최댓값이 곱해지지만)


## 2-SAT

2-satisfiability 문제.

n-satisfiability 문제의 가장 쉬운 케이스. or 로 연결된 부분의 갯수가 2인 경우.


Papadimitriou's 2-SAT algorithm 으로 풀 수 있다. (local search algorithm)

3-SAT 은 NP 문제이다.

SCC 알고리즘으로 풀 수도 있다.

back tracking 알고리즘도 있다. (하지만 정리 안해둠)
