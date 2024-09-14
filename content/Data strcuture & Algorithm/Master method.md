
> [!NOTE] 평범한 분할 정복 알고리즘의 성능 평가 도구
> ... 평범한 놈들만 적용된다.


# 가정


몇가지 가정이 필요하다.
- 같은 크기의 sub-problem 으로 나뉠 것.
- a, b 파라미터가 상수일 것.
- extra work function $f(n)$ 은 polynomial

# 적용 방법


다음과 같은 Recursion relation 이 주어졌을 때

$$
T(n) = a T\left(\frac{n}{b}\right) + f(n)   
$$
Critical exponent $c_{crit}$ 를 정의하고

$$
c_{crit} = \log_b{a}
$$
$f(n)\sim O(n^c)$ 라고 하자.

1. Heavy-leaf condition
$c\lt c_{crit}$ 일 때, 문제를 나누고 합하는 일이 상대적으로 가볍고, leaf 의 작업이 보틀넥이 된다.
$$
T(n) = \Theta(n^{c_{crit}})
$$

2. Steady condition
$f(n)= O(n^{c_{crit}}\log^{k}{n})$ 일 때, 
$$
T(n)=\Theta(n^{c_{crit}}log^{k +1}{n})
$$

좀 복잡한데, $f(n)$ polynomial 인 케이스가 많으므로 그 경우에만 따로 적는다면
$$
T(n)=\Theta(n^{c_{crit}}\log{n})
$$


3. Heavy-root condition
$c\gt c_{crit}$ 일 때, 문제를 나누고 합하는 일이 상대적으로 무겁고, root 의 작업이 보틀넥이 된다.
$$
T(n)=\Theta(f(n))
$$

일반적으로는 좀 더 복잡한데, regularity condition 에선 그렇다고 한다.

# 예시


각 케이스의 대표적인 예시들
1. Matrix multiplication
2. Merge sort, Binary search
3. 보통 잘못된 알고리즘임 (합치고 나누는데 힘이 너무 들면 분할 정복하는 의미가?)

처음 분할 정복을 봤을 때 $a$ 와 $b$ 가 같을 거라고 무의식적으로 생각했는데, 최적화를 위해 그렇지 않은 경우가 있고, Binary search 처럼 태생적으로 그런 경우도 있다.