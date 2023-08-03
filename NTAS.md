# NTAS-LOG

## 첫째날 ┐
## 　　 　├── 쿼드마이너 관리서버/분석서버 UI 조작(버튼 검색)
## 둘째날 ┘

## 셋째날 AQL실습 퀴즈
### 2023-08-02 14:45:000.000 퇴근 
```SQL
SELECT sourceip, sourceport, destinationip, destinatioport, count
FROM
events
WHERE destinatioport in (80, 443, 8080)
group by destinationport destinatioport desc
```




## 넷째날 SQL실습 퀴즈
### 2023-08-03 15:00:000.000 ~ 2023-08-03 15:30:000.000 퇴근

### Quiz.1
```SQL
SELECT
qidname(qid)
,logsourcename(logsourceid) as logsourcename
,utf8(payload)
,LONG(sourceport)
FROM
events
WHERE 
logsourcename like '%nbb-aio%'
AND
qidname(qid) like '%사용자룰%'
order by sourceport desc
limit 500
START '2023-08-02 14:00:00' 
STOP '2023-08-02 15:30:35'
```
### Quiz.2
```SQL
SELECT
logsourcename(logsourceid) as logsourcename
,qidname(qid)
,str(sourceip) as str_srcip
,STR(concat(sourceip,':',sourceport)) as "src"
,STR(concat(destinationip,':',destinationport)) as "dsc"
FROM
events
WHERE
logsourcename like '%nbb-aio%'
and str_srcip LIKE '%192.168%'
and dsc in LIKE '%50:80%'
limit 2000
START '2023-08-02 14:00:00' 
STOP '2023-08-02 16:00:00'
```
### Quiz.3
```SQL
SELECT
logsourcename(logsourceid) as logsourcename
,qidname(qid)
,DATEFORMAT(starttime,'yyyy-MM-dd hh:mm:ss')
,DATEFORMAT(devicetime,'yyyy-MM-dd hh:mm:ss') as devicetime
FROM
events
WHERE
logsourcename like '%nbb-aio%'
and devicetime between '2023-08-01 00:00:00' and '2023-08-01 23:00:00'
order by devicetime asc
limit 3000
START '2023-08-02 00:00:00' 
STOP '2023-08-03 00:00:00'
```
