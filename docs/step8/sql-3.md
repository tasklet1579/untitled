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

​

✍️ 프로그래머별로 해당하는 병원 이름을 반환하세요.

```
ALTER TABLE `subway`.`programmer` ADD PRIMARY KEY (`id`)
ALTER TABLE `subway`.`covid` ADD PRIMARY KEY (`id`)
ALTER TABLE `subway`.`hospital` ADD PRIMARY KEY (`id`)
ALTER TABLE `subway`.`covid` ADD INDEX `idx_programmer_id`(`programmer_id`)
ALTER TABLE `subway`.`covid` ADD INDEX `idx_hospital_id`(`hospital_id`)


SELECT C.id 
    ,  H.name 
  FROM subway.programmer P
 INNER JOIN subway.covid C 
    ON P.id = C.programmer_id 
 INNER JOIN subway.hospital H 
    ON C.hospital_id = H.id 
 ORDER BY P.id 


id |name   |
---|-------|
1  |고려대병원    |
2  |분당서울대병원 |
3  |경희대병원   |
4  |우리들병원   |
5  |우리들병원   |
...
```

​

✍️ 프로그래밍이 취미인 학생 혹은 주니어(0-2년)들이 다닌 병원 이름을 반환하고 user.id 기준으로 정렬하세요.

```


```

​

✍️ 서울대병원에 다닌 20대 India 환자들을 병원에 머문 기간별로 집계하세요.

```


```

​

✍️ 서울대병원에 다닌 30대 환자들을 운동 횟수별로 집계하세요.

```


```
