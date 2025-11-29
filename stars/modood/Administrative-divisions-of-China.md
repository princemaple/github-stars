---
project: Administrative-divisions-of-China
stars: 20280
description: 中华人民共和国行政区划：省级（省份）、 地级（城市）、 县级（区县）、 乡级（乡镇街道）、 村级（村委会居委会） ，中国省市区镇村二级三级四级五级联动地址数据。
url: https://github.com/modood/Administrative-divisions-of-China
---

Administrative-divisions-of-China
=================================

中华人民共和国行政区划（五级）：省级、地级、县级、乡级和村级。

数据来源
----

-   国家统计局：
    -   中华人民共和国国家统计局-统计用区划和城乡划分代码
    -   中华人民共和国国家统计局-统计用区划代码和城乡划分代码编制规则
-   本项目已更新至：
    -   2023年统计用区划代码和城乡划分代码（截止时间：2023-06-30，发布时间：2023-09-11）

数据下载
----

文件列表

JSON

CSV

省级（省份、直辖市、自治区）

provinces.json

provinces.csv

地级（城市）

cities.json

cities.csv

县级（区县）

areas.json

areas.csv

乡级（乡镇、街道）

streets.json

streets.csv

村级（村委会、居委会）

villages.json

villages.csv

文件列表

普通

带编码

“省份、城市” 二级联动数据

pc.json

pc-code.json

“省份、城市、区县” 三级联动数据

pca.json

pca-code.json

“省份、城市、区县、乡镇” 四级联动数据

pcas.json

pcas-code.json

“省份、城市、区县、乡镇、村庄” 五级联动数据

\-

\-

> 提示：需要打包下载全部文件，请看 Releases。

数据库支持
-----

目前本项目数据保存在 sqlite3，数据文件下载：data.sqlite。

可以自己将数据迁移到其他数据库管理系统中（MySQL, Oracle, MSSQL 等）。

**省级数据预览**

code

name

13

河北省

14

山西省

15

内蒙古自治区

45

广西壮族自治区

**地级数据预览**

code

name

provinceCode

1301

石家庄市

13

1401

太原市

14

1525

锡林郭勒盟

15

4503

桂林市

45

**县级数据预览**

code

name

cityCode

provinceCode

130111

栾城区

1301

13

140121

清徐县

1401

14

152527

太仆寺旗

1525

15

450305

七星区

4503

45

**乡级数据预览**

code

name

areaCode

cityCode

provinceCode

130111200

南高乡

130111

1301

13

140121102

东于镇

140121

1401

14

152527201

贡宝拉格苏木

152527

1525

15

450305004

漓东街道办事处

450305

4503

45

**村级数据预览**

code

name

streetCode

areaCode

cityCode

provinceCode

130111200201

南高村委会

130111200

130111

1301

13

140121102001

东于社区居委会

140121102

140121

1401

14

152527201206

敦达乌苏嘎查

152527201

152527

1525

15

450305004006

横塘社区

450305004

450305

4503

45
