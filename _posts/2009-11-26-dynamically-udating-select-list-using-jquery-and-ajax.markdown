--- 
wordpress_id: 58
layout: default
title: "Dynamically updating selectlist using Jquery and Ajax "
wordpress_url: http://railstech.com/?p=58
---
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :-Amar Daxini </span>
<br />
<hr />
In many web site we have seen that on selecting country,
state or city list is updated.In this article i am showing how to update children select list on changing parent list.
To do this i am using jquery and ruby on rails.although it will works for almost all languages
For this article, I am updating city list on changing states.
So one state has many cities,and city belongs to state.
<br />
{% highlight html%}
<html>
 <head>
   <script type="text/javascript" src="jquery.js"></script>
   <script type="text/javascript">
   $("#states").live("change",function(){
     state_id = $("#states").val();
     $.ajax({
       type: "GET",
       url: "/city_list.xxx",
        /*or any server side url which generate citylist for rails
                 "/states/city_list"or<%= city_list_states_path%> */
      data: "state_id="+state_id,
       /*here we are passing state_id to server based on that on
             he can find out  all the city related to that states */
     success: function(html){
      /*html content response of city_list.xxx */
     $("#city_list").html(html);
      }
    });
   });
 </script>
</head>
<body>
 <div id="state_list">
   <select id="states">
     <option>a</option>
     <option>b</option>
   </select>
 </div>
 <div id="city_list">
   <select id="cities">
   <option value="1">aa</option>
   <option value="2">aaa</option>
 </select>
 </div>
 </body>
</html>
{% endhighlight %}


and city_list.xxx  gives following html
on processing state id which we have pass as state_id

<br />

{% highlight html%}
<select id="cities">
  <option value="3">bb</option>
  <option value="4">bbb</option>
</select>
{% endhighlight %}
I have updated source code
<a href="http://github.com/amardaxini/Ajax-Demo">http://github.com/amardaxini/Ajax-Demo</a>
