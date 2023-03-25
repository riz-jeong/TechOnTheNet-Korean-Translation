## SQL : 데이터 형식

이 SQL 튜토리얼에서는 일반적인 SQL 데이터 형식 목록을 제공합니다. 이러한 데이터 형식은 모든 관계형 데이터베이스에서 지원되지 않을 수 있습니다.

| 데이터 형식 구문 | 설명 |
| :- | :- |
| integer | 정수(일반적으로 사용) |
| smallint | 작은 범위의 정수 |
| numeric(p,s) | p는 전체 자릿수 값이고, s는 소수 자릿수 값입니다. 예를 들어 numeric(6,2)는 소수점 앞에 4자리가 있고 소수점 뒤에 2자리가 있는 숫자입니다. |
| decimal(p,s) | p는 전체 자릿수 값이고, s는 소수 자릿수 값입니다. |
| real | 단정밀도 부동 소수점 |
| double precision | 배정밀도 부동 소수점 |
| float(p) | p는 정밀도 값입니다. |
| char(x) | x는 저장할 문자 수입니다. 이 데이터 형식은 지정된 문자 수를 채우기 위해 공백으로 채워집니다. |
| varchar(x) | x는 저장할 문자 수입니다. 이 데이터 형식은 공백을 사용하지 않습니다. |
| bit(x) | x는 저장할 비트 수입니다. |
| bit varying(x) | x는 저장할 비트 수입니다. 길이는 최대 x까지 다양할 수 있습니다. |
| date | 년, 월, 일 값을 저장합니다. |
| time | 시, 분, 초 값을 저장합니다. |
| timestamp | 년, 월, 일, 시, 분, 초 값을 저장합니다. |
| time with time zone | time과 정확히 동일하지만 지정된 시간의 UTC 오프셋도 저장합니다. |
| timestamp with time zone | timestamp와 정확히 동일하지만 지정된 시간의 UTC 오프셋도 저장합니다. |
| year-month interval | 년 값, 월 값 또는 둘 다를 포함합니다. |
| day-time interval | 일 값, 시간 값, 분 값 및/또는 초 값을 포함합니다. |

---
**[< 이전](EXCEPT.md) / [다음 : CREATE TABLE >](CREATE_TABLE.md)**