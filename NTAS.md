# NTAS-LOG


```SQL
SELECT sourceip, sourceport, destinationip, destinatioport, count
FROM
events
WHERE destinatioport in (80, 443, 8080)
group by destinationport destinatioport desc
```





### 2023-08-03 14:06:000.000

### 1.
```
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
### 2.
```
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
### 3.
```
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