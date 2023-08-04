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

## 마지막날 splunk 실습

1. 가장 많은 PC들이 질의한 도메인은 몇대의 PC가 질의하였는가?
2. 1번의 질의 도메인 주소는 무엇인가? (2개)
3. 'microsoft.com'이 포함되는 도메인 질의 (*.microsoft.com)는 몇개인가? 
4. 'microsoft.com'를 질의한 단말기의 운영체제는 무엇으로 추정되는가?
- ① Windows 계열 ② Linux 계열 ③ Mac OS 계열
5. 『z.arin.net』 도메인 질의에 관련하여 답하시오.
- 위의 도메인은 몇대에서(DC_src_ip) 몇일간 통신(COD)이 나왔는가?
- 『arin』의 Full name은? (인터넷 검색)
- Virustotal에서 해당 도메인에 대해서 검색했을때, 평판이 어떠한가?
(해당 문제에서는 특정 도메인의 DETECTION 탭 수만 보고 판단한다고 가정한다)
6. 어떤 소프트웨어 사용간 『update.joomla.org』 질의가 발생한다.
- 해당 프로그램을 사용하는 단말기는 몇 대로 추정되는가?
- 해당 프로그램의 용도는 무엇인가? (홈페이지 내 정보 탐색)
7. OO 악성코드에 감염된 PC는 4대라고 한다.
- 악성코드가 발생시킨것으로 추정되는 도메인은 무엇인가?
