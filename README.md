== ActiveRecord problem with 4.0.1.rc3 + mysql gem?

I'm aware that the `mysql` gem isn't the favorite vs. `mysql2`, but using it
with Rails 4.0.0 worked fine, and update to 4.0.1.rc3 broke for me.

App was created with typical progression:

```
rails new
rails generate model Order
rake db:create db:migrate
```

With those basics done, running this command results in the following error
while it succeeds on 4.0.0:

```
~/source/newrelic/support/rc3_issue: bundle exec rails runner 'Order.create'
/Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/railties-4.0.1.rc3/lib/rails/commands/runner.rb:53:in `eval': wrong number of arguments(1 for 0) (ArgumentError)
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/mysql_adapter.rb:562:in `set_field_encoding'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/abstract_mysql_adapter.rb:464:in `block (2 levels) in columns'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/mysql_adapter.rb:146:in `block in each_hash'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/mysql_adapter.rb:144:in `each_hash'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/mysql_adapter.rb:144:in `each_hash'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/abstract_mysql_adapter.rb:463:in `each'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/abstract_mysql_adapter.rb:463:in `map'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/abstract_mysql_adapter.rb:463:in `block in columns'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/mysql_adapter.rb:447:in `execute_and_free'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/abstract_mysql_adapter.rb:462:in `columns'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/schema_cache.rb:114:in `block in prepare_default_proc'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/schema_cache.rb:56:in `yield'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/schema_cache.rb:56:in `default'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/connection_adapters/schema_cache.rb:56:in `columns'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/model_schema.rb:208:in `columns'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/model_schema.rb:249:in `column_defaults'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/locking/optimistic.rb:169:in `column_defaults'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/core.rb:171:in `initialize'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/inheritance.rb:27:in `new'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/inheritance.rb:27:in `new'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/activerecord-4.0.1.rc3/lib/active_record/persistence.rb:36:in `create'
from (eval):1:in `<top (required)>'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/railties-4.0.1.rc3/lib/rails/commands/runner.rb:53:in `eval'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/railties-4.0.1.rc3/lib/rails/commands/runner.rb:53:in `<top (required)>'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/railties-4.0.1.rc3/lib/rails/commands.rb:84:in `require'
from /Users/jclark/.rbenv/versions/1.9.3-p374/lib/ruby/gems/1.9.1/gems/railties-4.0.1.rc3/lib/rails/commands.rb:84:in `<top (required)>'
from bin/rails:4:in `require'
from bin/rails:4:in `<main>'
```
