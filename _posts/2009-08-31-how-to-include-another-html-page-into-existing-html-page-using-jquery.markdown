--- 
wordpress_id: 30
layout: default
title: How to include another html page into existing html page using jquery
wordpress_url: http://railstech.com/?p=30
---
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />
We can include another html page using<span style="color: #3366ff;"> jquery </span> load method.<br />
Example is as shown below.

<br />

{% highlight html %}
<html xmlns="http://www.w3.org/1999/xhtml"> 
 <head> 
     <title>Loading an Html page</title>
     <script src="jquery.js" type="text/javascript"></script>
       $(document).ready(function() {
            $('#loadpage').load('load.html or any server side page');
        });
     </script>
 </head>
 <body>
    <div>loadpage</div> 
 </body>
</html>
{% endhighlight %}
<br />
