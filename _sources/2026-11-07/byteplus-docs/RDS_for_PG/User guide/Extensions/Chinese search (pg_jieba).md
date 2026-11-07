---
title: "Chinese search (pg_jieba)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_search-pg_jieba"
---

pg_jieba is a PostgreSQL extension for Chinese word segmentation full\-text search.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

pg_jieba not only provides basic word segmentation functions but also offers the capability for custom word segmentation. To use the custom word segmentation feature, pg_jieba must be added to the shared_preload_libraries parameter. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">It is recommended to make business plans and impact assessments in advance before modifying the parameters.</div>


<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   create extension pg_jieba;
   ```
   

* Delete extension

   ```sql
   drop extension pg_jieba;
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage


* Basic usage

   ```sql
   postgres=# select * from to_tsquery('jiebacfg', '是拖拉机学院手扶拖拉机专业的。不用多久，我就会升职加薪，当上CEO，走上人生巅峰。');
                                                               to_tsquery                                                            
   ----------------------------------------------------------------------------------------------------------------------------------
    '拖拉机' & '学院' & '手扶拖拉机' & '专业' & '不用' & '多久' & '会' & '升职' & '加薪' & '当上' & 'ceo' & '走上' & '人生' & '巅峰'
   (1 row)
   
   postgres=# select * from to_tsvector('jiebacfg', '是拖拉机学院手扶拖拉机专业的。不用多久，我就会升职加薪，当上CEO，走上人生巅峰。');
                                                                   to_tsvector                                                                 
   --------------------------------------------------------------------------------------------------------------------------------------------
    'ceo':18 '不用':8 '专业':5 '人生':21 '会':13 '加薪':15 '升职':14 '多久':9 '学院':3 '巅峰':22 '当上':17 '手扶拖拉机':4 '拖拉机':2 '走上':20
   (1 row)
   
   -- Token And Tag
   postgres=# select * from ts_token_type('jieba');
    tokid | alias |         description
   -------+-------+-----------------------------
        1 | eng   | letter
        2 | nz    | other proper noun
        3 | n     | noun
        4 | m     | numeral
        5 | i     | idiom
        6 | l     | temporary idiom
        7 | d     | adverb
        8 | s     | space
        9 | t     | time
       10 | mq    | numeral-classifier compound
       11 | nr    | person's name
       12 | j     | abbreviate
       13 | a     | adjective
       14 | r     | pronoun
       15 | b     | difference
       16 | f     | direction noun
       17 | nrt   | nrt
       18 | v     | verb
       19 | z     | z
       20 | ns    | location
       21 | q     | quantity
       22 | vn    | vn
       23 | c     | conjunction
       24 | nt    | organization
       25 | u     | auxiliary
       26 | o     | onomatopoeia
       27 | zg    | zg
       28 | nrfg  | nrfg
       29 | df    | df
       30 | p     | prepositional
       31 | g     | morpheme
       32 | y     | modal verbs
       33 | ad    | ad
       34 | vg    | vg
       35 | ng    | ng
       36 | x     | unknown
       37 | ul    | ul
       38 | k     | k
       39 | ag    | ag
       40 | dg    | dg
       41 | rr    | rr
       42 | rg    | rg
       43 | an    | an
       44 | vq    | vq
       45 | e     | exclamation
       46 | uv    | uv
       47 | tg    | tg
       48 | mg    | mg
       49 | ud    | ud
       50 | vi    | vi
       51 | vd    | vd
       52 | uj    | uj
       53 | uz    | uz
       54 | h     | h
       55 | ug    | ug
       56 | rz    | rz
   (56 rows)
   ```
   

* Advanced use \- Customize word segmentation effect

   After completing the prerequisites, the following parameters will take effect. These configuration options can help customize word segmentation effects to meet specific business needs.

   ```sql
   pg_jieba.hmm_model -- HMM Model file.
   pg_jieba.base_dict -- Base dictionary.
   pg_jieba.user_dict -- csv list of specific user dictionary name(Exclude suffix .dict). All should located in dir tsearch_data.
   ```
   


<span id=".5YW25LuW"></span>
## Others

For more information, please refer to [pg_jieba official documentation](https://github.com/jaiminpan/pg_jieba).
