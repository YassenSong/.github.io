# 亚森开发手册

[TOC]

## PostgreSql常用函数

### 1.类型转换

**1、cast（ a as numeric）函数**

`select cast(1 as numeric) as num;`

**2、双冒号 ::**

`elect 1::numeric as num;`

**3、保留小数部分 round()**

`select round(1::numeric/4::numeric,2);`

**4、关于 cast 函数的用法 substr 索引默认为1 下面是从 第3位开始，截取1位**

`SELECT substr(CAST (1234 AS text), 3,1); `

**5、把时间戳转换成字符串to_char(timestamp, text)**

`select to_char(now(),'YYYY/MM/DD');`

`select to_char(now(),'HH12:MI:SS');`

**6、把字符串转换成日期to_date(text,text)**

`select to_date('2019/12/19','YYYY/MM/DD');`

**7、把字符串转换成时间戳to_timestamp(text, text)**

`select to_timestamp('05 Jan 2015', 'DD Mon YYYY');`

**8、返回第一个非NULL的参数COALESCE()**

`select COALESCE (null,'');`

**9、比较两个元素是否相等NULLIF(value1, value2),如果不相等，返回第一个元素**

`select NULLIF(1,2);`

### 2.字符串处理

**1、字符串拼接  ||**

`select 'Post' || 'greSQL';`

**2、字符串的长度 length()**

`select length('PostgreSQL');`

**3、模式匹配 like**

`select * from t_zhba_mb_ws where c_mbmc like '%呈批表%';`

**4、连接字符串 concat()**

`select * from t_zhba_mb_ws where c_mbmc like concat('%','呈','批','表','%');`

**5、去重 distinct**

`select distinct on(c_mbbh) * from t_zhba_wssl;`

**6、拼接 string_agg（）**

`select sp.c_tqnr,string_agg(sp.c_dqztmc, '，' order by d_zhgx_sj desc)
from t_zhba_sp sp group by sp.c_tqnr`

**7、一行以逗号分隔的数据变多行regexp_split_to_table（）**

`select regexp_split_to_table(lc_wsid,';') as a from 
(select btrim(lc_wsid,';') as lc_wsid from t_zhba_rwsl where c_bh = '02C971B33F344BE3D94B7C27B60E84E8') as b`

**8、把字符串转化为小写lower( string )**

`select id a, lower(id) from t`

**9、把字符串转化为大写upper( string )**

``select id a, upper(id) from t``

**10、从字符串 string 的开头/结尾/两边删除只包含characters 中字符 (缺省是空白)的最长的字符串trim()**

`select trim(lc_wsid,';') from t_zhba_rwsl`

### 3.分组排序

**1、ROW_NUMBER() OVER(PARTITION BY COLUMN ORDER BY COLUMN)**

`select * from (select sp.c_bh,sp.c_dqztmc,row_number()over(partition by c_tqnr order by d_zhgx_sj) as tn from t_zhba_sp as sp )as t where t.tn = 1`;



## Git操作命令

### 1、将本地仓库推送到远端

- **初始化本地仓库**

  `git init`

- **提交所有文件到暂存区**

  `git add .`

- **推到本地仓库**

  `git commit -m “description”`

- **本地仓库和远程仓库建立连接**

  `git remote add origin https://github.com/YassenSong/documents.git`

- **推送到dev远程分支**

  `git push -u origin master`

### 2、git 清除缓存

- `git rm -r --cached .`
- `git add .`
- `git commit -m 'clear'`

### 3、其他常用命令

- **创建新分支**

  `git checkout -b chen origin/dev "chen"是创建本地的分支，"dev"是"chen"追踪的分支.`

- **查看分支**

  `git branch`

- **查看修改文件**

  `git status`

- **查看提交内容**

  `git log`

- **切换到分支dev**

  `git checkout dev`

- **拉取远程仓库所有分支更新并合并到本地**

  `git pull`

- **git commit后但是没有push的撤销方法**

  `git reset HEAD^ `

### 4、git版本回退

- **git回退到上个版本**

  `git reset --hard HEAD^ `

- **回退到前3次提交之前，以此类推，回退到n次提交之前**

  `git reset --hard HEAD~3`

- **退到/进到 指定commit的sha码**

  `git reset --hard dde8c25694f34acf8971f0782b1a676f39bf0a46 `

- **强推到远程**

  `git push origin HEAD --force`