---
annotation-target: Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf
---




>%%
>```annotation-json
>{"created":"2023-10-27T11:47:33.846Z","updated":"2023-10-27T11:47:33.846Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":145995,"end":146430},{"type":"TextQuoteSelector","exact":"ind the time zone observed by the server or what was requested. Suppose it’s“America/New_York” and get the offset for that period of time corresponding tothe UTC of the date time in question. For things that just have a time element liketimetz, the offset assumed—if not specified—is the current local time offset. Let’ssuppose it’s -5. You can also directly specify an offset instead of a time zone toavoid the Daylight Savings check.","prefix":" through the following steps:• F","suffix":"66 | Chapter 5: Data Typeswww.it"}]}]}
>```
>%%
>*%%PREFIX%%through the following steps:• F%%HIGHLIGHT%% ==ind the time zone observed by the server or what was requested. Suppose it’s“America/New_York” and get the offset for that period of time corresponding tothe UTC of the date time in question. For things that just have a time element liketimetz, the offset assumed—if not specified—is the current local time offset. Let’ssuppose it’s -5. You can also directly specify an offset instead of a time zone toavoid the Daylight Savings check.== %%POSTFIX%%66 | Chapter 5: Data Typeswww.it*
>%%LINK%%[[#^0oihjo535qeo|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^0oihjo535qeo


>%%
>```annotation-json
>{"created":"2023-10-27T11:54:56.701Z","updated":"2023-10-27T11:54:56.701Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":146869,"end":147025},{"type":"TextQuoteSelector","exact":"When PostgreSQL displays back the time, it always does so in thedefault time zone dictated by the session, user, database, or server and checks in thatorder","prefix":"t time zoneinformation is gone. ","suffix":". If you employed time zone awar"}]}]}
>```
>%%
>*%%PREFIX%%t time zoneinformation is gone.%%HIGHLIGHT%% ==When PostgreSQL displays back the time, it always does so in thedefault time zone dictated by the session, user, database, or server and checks in thatorder== %%POSTFIX%%. If you employed time zone awar*
>%%LINK%%[[#^z2jkudhf7ir|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^z2jkudhf7ir


>%%
>```annotation-json
>{"created":"2023-10-27T13:13:01.079Z","text":"Do note, however, that the actual storage of a timestamptz does not store any time zone data. It stores all values in UTC. The time zone aspect comes into play when inputting and outputting the timestamp data. When you input a timestamptz, PostgreSQL will assume the timestamp is in the time zone set by the TimeZone configuration parameter, and it will convert it to UTC for storage. When you retrieve a timestamptz, PostgreSQL will convert the UTC value to the time zone specified by the TimeZone parameter before displaying it.","updated":"2023-10-27T13:13:01.079Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}
>```
>%%
>*%%PREFIX%%%%HIGHLIGHT%% ==== %%POSTFIX%%*
>%%LINK%%[[#^b64wcnsgqu4|show annotation]]
>%%COMMENT%%
>Do note, however, that the actual storage of a timestamptz does not store any time zone data. It stores all values in UTC. The time zone aspect comes into play when inputting and outputting the timestamp data. When you input a timestamptz, PostgreSQL will assume the timestamp is in the time zone set by the TimeZone configuration parameter, and it will convert it to UTC for storage. When you retrieve a timestamptz, PostgreSQL will convert the UTC value to the time zone specified by the TimeZone parameter before displaying it.
>%%TAGS%%
>#postgres
^b64wcnsgqu4


>%%
>```annotation-json
>{"created":"2023-10-27T13:15:53.583Z","updated":"2023-10-27T13:15:53.583Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":151523,"end":151585},{"type":"TextQuoteSelector","exact":"OVERLAPS Returnstrue or false if two tem-poral ranges overlap.","prefix":" '1 hour';2012-02-10 22:00:00-05","suffix":"This is an ANSI-SQL op-erator eq"}]}]}
>```
>%%
>*%%PREFIX%%'1 hour';2012-02-10 22:00:00-05%%HIGHLIGHT%% ==OVERLAPS Returnstrue or false if two tem-poral ranges overlap.== %%POSTFIX%%This is an ANSI-SQL op-erator eq*
>%%LINK%%[[#^hfbvft6yqs|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^hfbvft6yqs


>%%
>```annotation-json
>{"created":"2023-10-27T13:46:35.929Z","updated":"2023-10-27T13:46:35.929Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":156776,"end":156999},{"type":"TextQuoteSelector","exact":" Thecomposite, (a.k.a. record, row) object type is a special type in PostgreSQL because it’soften used to build an object that is then cast to a custom type or as return types forfunctions needing to return multiple columns","prefix":"a simple custom type and use it.","suffix":".All Tables Are CustomAs mention"}]}]}
>```
>%%
>*%%PREFIX%%a simple custom type and use it.%%HIGHLIGHT%% ==Thecomposite, (a.k.a. record, row) object type is a special type in PostgreSQL because it’soften used to build an object that is then cast to a custom type or as return types forfunctions needing to return multiple columns== %%POSTFIX%%.All Tables Are CustomAs mention*
>%%LINK%%[[#^8ap5ip57ywh|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^8ap5ip57ywh


>%%
>```annotation-json
>{"created":"2023-10-27T19:21:51.984Z","updated":"2023-10-27T19:21:51.984Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":158622,"end":158997},{"type":"TextQuoteSelector","exact":"CREATE TYPE complex_number AS (r double precision, i double precision);We can then use this complex_number as a column type:CREATE TABLE circuits(circuit_id text PRIMARY KEY, tot_volt complex_number);We can then query our table with statements such as:SELECT circuit_id, (tot_volt).*  FROM circuits;or an equivalent:SELECT circuit_id, (tot_volt).r, (tot_volt).i FROM circuits","prefix":"ata Types | 71www.it-ebooks.info","suffix":";People from other databases are"}]}]}
>```
>%%
>*%%PREFIX%%ata Types | 71www.it-ebooks.info%%HIGHLIGHT%% ==CREATE TYPE complex_number AS (r double precision, i double precision);We can then use this complex_number as a column type:CREATE TABLE circuits(circuit_id text PRIMARY KEY, tot_volt complex_number);We can then query our table with statements such as:SELECT circuit_id, (tot_volt).*  FROM circuits;or an equivalent:SELECT circuit_id, (tot_volt).r, (tot_volt).i FROM circuits== %%POSTFIX%%;People from other databases are*
>%%LINK%%[[#^mf7kytke9gb|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^mf7kytke9gb


>%%
>```annotation-json
>{"created":"2023-10-27T19:46:09.291Z","updated":"2023-10-27T19:46:09.291Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":161963,"end":162523},{"type":"TextQuoteSelector","exact":"CREATE TABLE logs_2011(PRIMARY KEY(log_id)) INHERITS (logs);CREATE INDEX idx_logs_2011_log_ts ON logs USING btree(log_ts);ALTER TABLE logs_2011   ADD CONSTRAINT chk_y2011    CHECK (log_ts BETWEEN '2011-01-01'::timestamptz AND '2012-1-1'::timestamptz);We defined a check constraint to limit data to just year 2011 for our time zone. Sincewe didn’t specify a time zone, our timestamp will default to the server’s time zone.Having the check constraint in place allows the query planner to completely skipover inherited tables that do not satisfy a query condition","prefix":"le 6-2. Inherited table creation","suffix":".For ephemeral data that could b"}]}]}
>```
>%%
>*%%PREFIX%%le 6-2. Inherited table creation%%HIGHLIGHT%% ==CREATE TABLE logs_2011(PRIMARY KEY(log_id)) INHERITS (logs);CREATE INDEX idx_logs_2011_log_ts ON logs USING btree(log_ts);ALTER TABLE logs_2011   ADD CONSTRAINT chk_y2011    CHECK (log_ts BETWEEN '2011-01-01'::timestamptz AND '2012-1-1'::timestamptz);We defined a check constraint to limit data to just year 2011 for our time zone. Sincewe didn’t specify a time zone, our timestamp will default to the server’s time zone.Having the check constraint in place allows the query planner to completely skipover inherited tables that do not satisfy a query condition== %%POSTFIX%%.For ephemeral data that could b*
>%%LINK%%[[#^wex6kn1xxsj|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^wex6kn1xxsj


>%%
>```annotation-json
>{"created":"2023-10-27T19:58:58.221Z","updated":"2023-10-27T19:58:58.221Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":172259,"end":172494},{"type":"TextQuoteSelector","exact":"PostgreSQL query planner also uses them for what is called constraint exclusion which means if a check constraint on a table guarantees that it can’t service thefilter condition of a query, then the planner can skip checking the table.","prefix":"d or set of fields for eachrow. ","suffix":" We saw anexample of a check con"}]}]}
>```
>%%
>*%%PREFIX%%d or set of fields for eachrow.%%HIGHLIGHT%% ==PostgreSQL query planner also uses them for what is called constraint exclusion which means if a check constraint on a table guarantees that it can’t service thefilter condition of a query, then the planner can skip checking the table.== %%POSTFIX%%We saw anexample of a check con*
>%%LINK%%[[#^j03mob5xrn7|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^j03mob5xrn7


>%%
>```annotation-json
>{"created":"2023-10-27T20:16:52.650Z","updated":"2023-10-27T20:16:52.650Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":179114,"end":179386},{"type":"TextQuoteSelector","exact":"For instance, varchar_ops doesn’t include theLIKE operators, so none of your like searches can use an index of that opclass. If you’regoing to be performing wildcard searches on a varchar columns, you’d be better offchoosing the varchar_pattern_ops opclass for your index.","prefix":"dn’t always accept the default. ","suffix":" To specify the opclass, justapp"}]}]}
>```
>%%
>*%%PREFIX%%dn’t always accept the default.%%HIGHLIGHT%% ==For instance, varchar_ops doesn’t include theLIKE operators, so none of your like searches can use an index of that opclass. If you’regoing to be performing wildcard searches on a varchar columns, you’d be better offchoosing the varchar_pattern_ops opclass for your index.== %%POSTFIX%%To specify the opclass, justapp*
>%%LINK%%[[#^tq5wq2txbq|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^tq5wq2txbq


>%%
>```annotation-json
>{"created":"2023-10-27T20:18:29.901Z","updated":"2023-10-27T20:18:29.901Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":180526,"end":180630},{"type":"TextQuoteSelector","exact":"To still reap the speed advantage of indexes, Post-greSQL lets you place indexes on functions of columns","prefix":"re appropriate places for them. ","suffix":". A classic example where you’dw"}]}]}
>```
>%%
>*%%PREFIX%%re appropriate places for them.%%HIGHLIGHT%% ==To still reap the speed advantage of indexes, Post-greSQL lets you place indexes on functions of columns== %%POSTFIX%%. A classic example where you’dw*
>%%LINK%%[[#^fsfx5qsdbsm|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^fsfx5qsdbsm


>%%
>```annotation-json
>{"created":"2023-10-28T04:15:25.903Z","updated":"2023-10-28T04:15:25.903Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":185179,"end":185337},{"type":"TextQuoteSelector","exact":"Unlike Microsoft SQL Server and MySQL, simple views are not automatically updat-able and require writing an instead-of rule or trigger to make them updatable.","prefix":"rt triggers and updatable views.","suffix":" On theplus side, you have great"}]}]}
>```
>%%
>*%%PREFIX%%rt triggers and updatable views.%%HIGHLIGHT%% ==Unlike Microsoft SQL Server and MySQL, simple views are not automatically updat-able and require writing an instead-of rule or trigger to make them updatable.== %%POSTFIX%%On theplus side, you have great*
>%%LINK%%[[#^kg37o2rr9u|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^kg37o2rr9u


>%%
>```annotation-json
>{"created":"2023-10-28T08:12:11.107Z","updated":"2023-10-28T08:12:11.107Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":190191,"end":190370},{"type":"TextQuoteSelector","exact":"When PostgreSQL sees a window function in a particular row,it will actually scan all rows fitting the WHERE clause, perform the aggregation, and outputthe value as part of the row","prefix":"functioninto a window function. ","suffix":".Partition ByYou can embellish t"}]}]}
>```
>%%
>*%%PREFIX%%functioninto a window function.%%HIGHLIGHT%% ==When PostgreSQL sees a window function in a particular row,it will actually scan all rows fitting the WHERE clause, perform the aggregation, and outputthe value as part of the row== %%POSTFIX%%.Partition ByYou can embellish t*
>%%LINK%%[[#^1f4mba9i6ff|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^1f4mba9i6ff


>%%
>```annotation-json
>{"created":"2023-10-29T07:21:34.883Z","updated":"2023-10-29T07:21:34.883Z","document":{"title":"PostgreSQL: Up and Running","link":[{"href":"urn:x-pdf:e54399e2c59624bd477f98ecbf997880"},{"href":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf"}],"documentFingerprint":"e54399e2c59624bd477f98ecbf997880"},"uri":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","target":[{"source":"vault:/Resources/Databases/Postgresql/PostgreSQL Up and Running/Regina Obe, Leo Hsu - PostgreSQL_ Up and Running_ A Practical Guide to the Advanced Open Source Database-O'Reilly Media (2012).pdf","selector":[{"type":"TextPositionSelector","start":196116,"end":196274},{"type":"TextQuoteSelector","exact":"In its essence, common table expressions (CTE) allow you to assign a temporary variablename to a query definition so that it can be reused in a larger query. ","prefix":"X() etc.Common Table Expressions","suffix":"PostgreSQL hassupported this fea"}]}]}
>```
>%%
>*%%PREFIX%%X() etc.Common Table Expressions%%HIGHLIGHT%% ==In its essence, common table expressions (CTE) allow you to assign a temporary variablename to a query definition so that it can be reused in a larger query.== %%POSTFIX%%PostgreSQL hassupported this fea*
>%%LINK%%[[#^zja8jrkigzb|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^zja8jrkigzb
