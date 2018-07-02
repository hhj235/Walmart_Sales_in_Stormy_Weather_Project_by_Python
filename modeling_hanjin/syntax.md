# 데이트 타임 처리
`import datetime`
```
dt = datetime.datetime.now()
dt
```
`datetime.datetime(2018, 6, 10, 15, 31, 58, 660162)`
now() 클래스 메서드는 컴퓨터의 현재 시각을 datetime.datetime 클래스 객체로 만들어 반환한다. datetime.datetime 클래스 객체는 다음과 같은 속성을 가진다.
- year: 연도
- month: 월
- day: 일
- hour: 시
- minute: 분
- second: 초
- microsecond: 마이크로초(micro seconds, 백만분의 일초)

`dt.year, dt.month, dt.day, dt.hour, dt.minute, dt.second, dt.microsecond`
`(2018, 6, 10, 15, 31, 58, 660162)`

- weekday(): 요일 반환 (0:월, 1:화, 2:수, 3:목, 4:금, 5:토, 6:일)
- strftime(): 문자열 반환
- date(): 날짜 정보만 가지는 datetime.date 클래스 객체 반환
- time(): 시간 정보만 가지는 datetime.time 클래스 객체 반환

# dateutil 패키지
datetime.datetime.strptime() 클래스 메서드를 사용할 때는 문자열에 맞는 형식 문자열을 사용자가 제공해야 한다. 그러나 dateutil 패키지의 parse 명령을 쓰면 자동으로 형식 문자열을 찾아 datetime.datetime 클래스 객체를 만들어 준다.

`from dateutil.parser import parse`
`parse('2016-04-16')`
> datetime.datetime(2016, 4, 16, 0, 0)

`parse("Apr 16, 2016 04:05:32 PM")`
> datetime.datetime(2016, 4, 16, 16, 5, 32)

`parse('6/7/2016')`
> datetime.datetime(2016, 6, 7, 0, 0)

# 판다스 조건 필터
1. 기본적인 조건은  `df[df['cdsStart'] > 10000]`와 같이 걸어준다.

2. 2가지 이상의 조건은 `dfRefflat[(dfRefflat['cdsStart'] > 10000) & (dfRefflat['cdsEnd'] < 20000)]`와 같이 적용하면 된다. ()에 조건을 넣고 각 조건들 사이의 관계는 & (and), | (or) , == (equal), != (not)등으로 지정해줄 수 있다.

# 판다스 nan 값 찾아서 갯수 세기
`pd.isnull(df_weather['heat']).sum()`

# 판다스 조건문을 걸어 값 넣기
`df_weather['handled_heat'] = np.where(pd.notnull(df_weather['heat']) == True, df_weather['heat'], 65 + df_weather['tavg'])`

# 판다스 결측값 넣기
`df.interpolate()`
옵션에 따라 선형,비선형등 nan 값을 처리할 수 있음

# 판다스 sort하기
`data = data.sort_values(["time"], ascending=[False])`
`data.reset_index(drop=True)`

# 판다스 다중 조건 필터
```import numpy as np
import functools
def conjunction(*conditions):
    return functools.reduce(np.logical_and, conditions)

c_1 = data.col1 == True
c_2 = data.col2 < 64
c_3 = data.col3 != 4

data_filtered = data[conjunction(c1,c2,c3)]```



# 날짜/시간 연산
