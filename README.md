![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 快速检查复制
#### Quickly Check For SQL Replication
**发布-日期: 2017年10月16日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
想要快速检查数据库服务器是否配置了复制？ 试试下面这段SQL逻辑（Logic）。


## English
Want to quickly check to see if your Database Server has Replication configured? Try this little bit of SQL Logic.

---
## Logic
```SQL
use master;
set nocount on
 
--check if database server has replication configured at all
--检查数据库服务器是否完全配置了复制
 
select
     'sql_instance'     = upper(@@servername)
,    'has_replication'  = case when sum(cast(sd.is_published as int) + cast(sd.is_subscribed as int)) > 0 then 'Yes' else 'No' end
from
    sys.databases sd
 
--check which databases are involved in replication
--检查复制中涉及哪些数据库
select
    'database'      = upper(sd.name)
,   'published'     = case sd.is_published      when 0 then 'no' else 'yes' end
,   'published_merge'   = case sd.is_merge_published    when 0 then 'no' else 'yes' end
,   'distributor'   = case sd.is_distributor    when 0 then 'no' else 'yes' end
,   'subscriber'    = case sd.is_subscribed     when 0 then 'no' else 'yes' end
from
    sys.databases sd
where
    database_id > 4
order by sd.name asc


```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

