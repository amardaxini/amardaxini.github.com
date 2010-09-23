--- 
wordpress_id: 89
layout: default
title: Static pages in rails
wordpress_url: http://railstech.com/?p=89
---
{% include post-nav.textile %}
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />

<h2>Static site using rails</h2>
As we know rails is mainly used for <strong>dynamic website</strong>.we can also display <strong>static web pages</strong> or  we can deploy full <strong>static website</strong> using <strong>rails</strong>.  The following code can help us to display static pages.


<br />

<h3>Step 1:-Create Rails project</h3>

{% highlight ruby %}

rails static_site

{% endhighlight %}

<br />

<h3>Step 2:-Generate StaticPage Controller</h3>

{% highlight ruby %}
  ruby script/generate controller static_pages page
{% endhighlight %}


<br />

<h3>Step 3:- Create StaticPage Class in Model</h3>

{% highlight ruby %}
 class StaticPage
   Formats = {
       "html" => "text/html",
       "png" => "image/png",
       "jpg" => "image/jpg"
     }
 end

{% endhighlight %}

<br />

<h3>Step 4:- Add following line in routes.rb</h3>

{% highlight ruby %}

map.page "page/:filename.:format", :controller => 'static_pages', :action => 'page'

{% endhighlight %}

<br />

Here we are passing filename as parameter which is static file name.

This will generate <strong>url</strong> as<strong> http://sitename/page/static_filename.html</strong>

<br />
<h3>Step 5:- Now add following line into static_pages controller</h3>

{% highlight ruby %}

def page
 send_file
 "#{Rails.root}/app/views/static_pages/#{params[:filename]}.#{params[:format]}",:disposition =>'inline',:type => StaticPage::Formats[params[:format]]
 end
{% endhighlight %}


<br />

<h3>Step 6:- All the static pages place in RAILS_ROOT/app/views/static_pages/ folder</h3>
<br />
<h3>Step 7 :- Start server and Type url as shown below.</h3>

{% highlight ruby %}

ruby script/server

{% endhighlight %}

<br />

Url may be


<strong><a href="http://railstech.com/?page_id=2"> http://railstech.com/page/contactus.html</a></strong>

<br />

<strong><a href="http://railstech.com">http://railstech.com/page/faq.html</a> </strong>


