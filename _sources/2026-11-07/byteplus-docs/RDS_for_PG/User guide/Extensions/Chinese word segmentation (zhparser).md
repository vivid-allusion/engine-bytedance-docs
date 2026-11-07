---
title: "Chinese word segmentation (zhparser)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_word_segmentation-zhparser"
---

PostgreSQL comes with a parser extension suitable for languages where word segmentation is relatively simple (such as English), where meaningful words can be obtained by splitting sentences according to punctuation and spaces. However, Chinese is more complex, with no spaces between words and inconsistent lengths; word segmentation is also related to semantics, hence the parser cannot be used for Chinese word segmentation, and it is suggested to use zhparser. zhparser is a Chinese word segmentation extension for PostgreSQL, which, once installed, enables PostgreSQL to support full\-text search in Chinese.

<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION zhparser;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION zhparser;
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage


* Basic usage

   ```sql
   -- View Zhparser dictionary configuration
   SELECT ts_token_type('zhparser');
             ts_token_type          
   ---------------------------------
    (97,a,"adjective,形容词")
    (98,b,"differentiation,区别词")
    (99,c,"conjunction,连词")
    (100,d,"adverb,副词")
    (101,e,"exclamation,感叹词")
    (102,f,"position,方位词")
    (103,g,"root,词根")
    (104,h,"head,前连接成分")
    (105,i,"idiom,成语")
    (106,j,"abbreviation,简称")
    (107,k,"tail,后连接成分")
    (108,l,"tmp,习用语")
    (109,m,"numeral,数词")
    (110,n,"noun,名词")
    (111,o,"onomatopoeia,拟声词")
    (112,p,"prepositional,介词")
    (113,q,"quantity,量词")
    (114,r,"pronoun,代词")
    (115,s,"space,处所词")
    (116,t,"time,时语素")
    (117,u,"auxiliary,助词")
    (118,v,"verb,动词")
    (119,w,"punctuation,标点符号")
    (120,x,"unknown,未知词")
    (121,y,"modal,语气词")
    (122,z,"status,状态词")
   (26 rows)
   
   -- Configure Chinese parser
   CREATE TEXT SEARCH CONFIGURATION testzhcfg (PARSER = zhparser);
   
   -- Add six tokenization strategies for nouns (n), verbs (v), adjectives (a), idioms (i), exclamations (e), and set phrases (l);
   ALTER TEXT SEARCH CONFIGURATION testzhcfg ADD MAPPING FOR n,v,a,i,e,l WITH simple;
   
   -- Test tokenization effect (to_tsvector);
   SELECT to_tsvector('testzhcfg','BytePlus云数据库 PostgreSQL 版是一种即开即用、稳定可靠、灵活弹性、易于使用的关系型数据库服务。');
                                                                          to_tsvector                                                                        
   ----------------------------------------------------------------------------------------------------------------------------------------------------------
    'postgresql':4 '云':2 '使用':16 '即':7,9 '可靠':12 '开':8 '弹性':14 '数据库':3,17 '易于':15 '是':6 '服务':18 'BytePlus':1 '灵活':13 '版':5 '用':10 '稳定':11
   (1 row)
   
   --Test tokenization effect (to_tsquery);
   SELECT to_tsquery('testzhcfg', 'RDS-for-PostgreSQL完全兼容原生PostgreSQL，提供易用的管理界面与工具，方便用户以云模式使用和管理数据库');
                                                                                    to_tsquery                                                                                 
   ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    'rds-for-postgresql' & '完全' & '兼容' & '原生' & 'postgresql' & '提供' & '易用' & '管理' & '界面' & '工具' & '方便' & '用户' & '云' & '模式' & '使用' & '管理' & '数据库'
   (1 row)
   ```
   

* Advanced use—Utilize tokenization for full text indexing

   The following example creates a full\-text index for the introduce field of the test table. When using it, replace the table name (test) and field (introduce) in the SQL statement with the table name and field value in the actual business.

   ```sql
   -- Create test table;
   CREATE TABLE test(introduce text);
   INSERT INTO test VALUES ('使用RDS for PostgreSQL数据库，客户无需再关心底层硬件资源，降低使用成本，提高整体效率');
   INSERT INTO test VALUES ('兼容多种开源的插件，用户自由化管理，不同的数据类型及索引类型支持多种应用场景');
   INSERT INTO test VALUES ('按需开通，即开即用，灵活升降配置，与PostgreSQL原生接口一致，无需应用改造，全托管，免运维');
   -- Create index;
   CREATE INDEX idx ON test USING gin (to_tsvector('testzhcfg',upper(introduce)));
   -- Use full text index;
   SELECT * FROM test WHERE to_tsvector('testzhcfg',upper(test.introduce)) @@ to_tsquery('testzhcfg','(免运维)') ;
                                           introduce                                         
   ------------------------------------------------------------------------------------------
    按需开通，即开即用，灵活升降配置，与PostgreSQL原生接口一致，无需应用改造，全托管，免运维
   (1 row)
   ```
   


<span id=".5YW25LuW"></span>
## Others

For more information, please refer to the [zhparser official documentation](https://github.com/amutu/zhparser).
