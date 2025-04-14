
SQL 짤 때 영리하게 짜기 - case study

# new Insert - old update

새 레코드를 넣으며 기존 레코드를 deprecate 시키거나, 특정 날짜로 만료하는 유즈케이스.

특히 특정 주기로 바뀌는 형식의 데이터라면, 바뀌지 않는 데이터도 만료시키고 수정하는게 편할수도 있다.

동일한 데이터가 여럿 생기는 단점이 생길수도 있지만 작업 실수가 적어진다.

만약 변경분을 발라내야 한다면, 그 부분만 발라낼 수 있는 쿼리가 있어야 한다.

오늘 했던 작업도 quasi-key 가 있었는데 사용안했다. 반성반성


# Self join

데이터들 사이의 어떤 contraint 가 있는 경우 self join 을 사용해 검증하는게 직관적이다.


# group by, having 등으로 검증

데이터 통계에 contraint 가 있는 경우 (특정 상황에서만 uniqueness 가 있다던지) 검증 쿼리 짜는데 쓰일 수 있다.

예를 들면 한달에 두 레코드만 있어야 한다면 `group by MONTH() having COUNT(MONTH()) != 2` 같은 식으로 골라내는 식.


