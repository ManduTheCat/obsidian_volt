```  sql
-- 리두 로그 확인

SELECT a.GROUP#, a.TYPE, a.MEMBER, b.bytes/1024/1024 "MB",b.archived, b.status

FROM v$logfile a, v$log b

WHERE a.GROUP# = b.GROUP#

ORDER BY a.GROUP#;

  


```