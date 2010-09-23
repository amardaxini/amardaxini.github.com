--- 
wordpress_id: 53
layout: default
title: Select/Deselect Multiple CheckBox Using Jquery
wordpress_url: http://railstech.com/?p=53
---
{% include post-nav.textile %}
<h1 class="page-title">Select/Deselect Multiple CheckBox Using Jquery</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />
In many website we have seen that on checked or unchecked one box<br />
all the check box are checked or unchecked.<br />
Now in this article i am showing how to checked  unchecked  all the check box <br />

<br />
{% highlight html %}
<html>
  <head>
    <script type="text/javascript" src="jquery.js"></script>
    <script type="text/javascript">
     	$("#check_all").live("click",function(event)
	    {
		    if($("#check_all").hasClass('not_checked'))
		    {
			    $("#check_all").removeClass('not_checked');
			    $(".check-box").attr('checked',true);
		    }
		    else
		    {
			    $("#check_all").addClass('not_checked');
			    $(".check-box").attr('checked',false);
		    }
	  });
    </script>
  </head>
  <body>
    <table>
      <tr>
        <td>Select/Deselect</td>
        <td><input type="checkbox" class="check-box not_checked" id="check_all"></td>
      </tr>
      <tr>
        <td>First</td>
        <td><input type="checkbox" class="check-box" id="check_box2"></td>
      </tr>
      <tr>
        <td>Second</td>
        <td><input type="checkbox" class="check-box" id="check_box3"></td>
       </tr>
       <tr>
         <td>Third</td>
         <td><input type="checkbox" class="check-box" id="check_box4"></td>
      </tr>
    </table>
  </body>
</html>
{% endhighlight %}
<br />

In this setting checked attribute true/false alternatively by clicking on
select/deselect for alternate removing and adding class
not_checked depending upon that we are setting true and false

