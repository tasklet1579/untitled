✍️ Coding as a Hobby 와 같은 결과를 반환하세요.

```
SELECT P1.hobby
    ,  CONCAT(COUNT(1) / P2.Total * 100, '%') Percentage
  FROM subway.programmer P1
    ,  (SELECT COUNT(1) Total FROM subway.programmer) P2
 GROUP BY P1.hobby
        , P2.Total


hobby|Percentage|
-----|----------|
No   |19.1776%  |
Yes  |80.8224%  |
```

✍️ 프로그래머별로 해당하는 병원 이름을 반환하세요.

```


```

✍️ 프로그래밍이 취미인 학생 혹은 주니어(0-2년)들이 다닌 병원 이름을 반환하고 user.id 기준으로 정렬하세요.

```


```

✍️ 서울대병원에 다닌 20대 India 환자들을 병원에 머문 기간별로 집계하세요.

```


```

✍️ 서울대병원에 다닌 30대 환자들을 운동 횟수별로 집계하세요.

```


```
