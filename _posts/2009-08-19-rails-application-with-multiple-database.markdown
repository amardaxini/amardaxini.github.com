--- 
wordpress_id: 13
layout: default
title: Multiple database in rails
wordpress_url: http://railstech.com/?p=13
---
{% include post-nav.textile %}

<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />
In normal rails application contain one database,but if we want rails application having more than one database that is multiple data base.<br /> 
we can achieve this using multiple way.one of the way is i am showing here.it's just 3 steps.
<br />

Lets take an e.g Project has many milestone and milestone has many task
<br />
In normal scenario model looks like following way
<br />

{% highlight ruby %}
class Project < ActiveRecord::Base
  has_many :milestones
end

class Milestone < ActiveRecord::Base
    has_many :tasks
    belongs_to :project
end

class Task < ActiveRecord::Base
  belongs_to :milestone
end

  {% endhighlight %}
  <br />


Now we want that milestone is stored on milestone_db database and task on task_db database<br />
<img class="alignnone size-full wp-image-9" title="Rails multiple database" src="/images/posts/multipledatabase.png" alt="Rails multiple database" width="462" height="290" />
Now to achieve this we have to do the following steps<br />

1 Edit Database.yml

 {% highlight yaml %}
    milestone_dev:
     reconnect: false
     encoding: utf8
     username: <user_name>
     adapter: mysql
     database: milestone_db
     pool: 5
     password: <password>

    task_dev:
     reconnect: false
     encoding: utf8
     username: <user_name>
     adapter: mysql
     database: task_db
     pool: 5
     password: <password>
   {% endhighlight %}
   <br />
2 Edit milestone.rb and task.rb
{% highlight ruby %}

class Milestone < ActiveRecord::Base
  #add this line to use milestone_db
  self.establish_connection :milestone_dev
  has_many :tasks
  belongs_to :project
end

class Task < ActiveRecord::Base
  #add this line to use task_db
  set_table_name "tasks"
  belongs_to :milestone
end
 {% endhighlight %}
 <br />
3 After editing model edit migration file
{% highlight ruby %}
class CreateMilestones < ActiveRecord::Migration
  def self.connection
    Milestone.connection
  end
 .....
end
 {% endhighlight %}
<br />
Now rails application is ready with multiple database.


