---
layout: post
title: "disable active record migrations for specs"
date: 2014-03-26 13:15:01
categories:
---

I began working with a legacy database for which there are no migrations.

After I setup my Rails app and verified the database connection in Rails console I began writing my first integration test.
When I ran rspec it failed with a long exception whining about there being no SCHEMA_MIGRATIONS table.

```
  ActiveRecord::StatementInvalid: ActiveRecord::JDBCError: java.sql.SQLSyntaxErrorException: ORA-00942: table or view does not exist
  : SELECT "SCHEMA_MIGRATIONS".* FROM "SCHEMA_MIGRATIONS"
```

After a little grepping about I discovered the source of the problem in the default spec_helper.rb that rspec generated for me.

I deleted the following line and the spec ran as expected.

```
  ActiveRecord::Migration.check_pending! if defined?(ActiveRecord::Migration)
```
