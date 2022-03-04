# 1日あたりの打鍵量及びプレイ時間の計算

```sql
select * from (select (epg+lpg+egr+lgr+egd+lgd) - lag((epg+lpg+egr+lgr+egd+lgd), 1) over (order by date) as notes
	  , strftime('%Y-%m-%d', datetime(date,'unixepoch', '+9 hours')) as PlayDate
	  , playtime - lag(playtime) over (order by date) as dayofplaytime
from player
order by date) 
where notes not null
```

- dayofplaytime 秒
