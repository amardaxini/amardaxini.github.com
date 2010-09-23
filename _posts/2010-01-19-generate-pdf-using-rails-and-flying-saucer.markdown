--- 
wordpress_id: 73
layout: default
title: Generate PDF Using Rails and Flying Saucer
wordpress_url: http://railstech.com/?p=73
---
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />
<h2>Rails Pdf Plugin act_as_flying_saucer</h2>
There are various ways to generate pdf documents in any language.In Rails we can use prawn library ,HtmlDoc,PrinceXml  and many other library,using their api we can generate pdf  document.Basically  the primary goal is converting HTML web pages to PDF Document,without much changing existing CSS and HTML.

<br />
Using the<a href="https://xhtmlrenderer.dev.java.net/" target="_blank"> Flying Saucer Project</a> we can achieve this.we can convert  HTML + CSS to PDF documents without much changing HTML and CSS. It also support CSS  2 and many properties of CSS 3 for  printing Header,Footer,Page Number,Paginated Tables and many more.This Project is built on Java so Java is required on system.

<br />

Lets Start How to generate PDF Using Flying Saucer.

<br />

{% highlight ruby %}
 script/plugin install git://github.com/amardaxini/acts_as_flying_saucer.git
{% endhighlight %}

<br />

This Plugin forked From

{% highlight html %}http://github.com/dagi3d/acts_as_flying_saucer{% endhighlight %}

Which has older version of flying saucer project.

<br />

Next Step after installing plugin add <strong>flying_saucer.rb </strong> file at <strong>config/initializers</strong>.

<br />

{% highlight ruby %}

ActsAsFlyingSaucer::Config.options = {
:java_bin => "/usr/bin/java",          # java binary
:classpath_separator => ':',           # classpath separator. unixes system use ':' and windows ';'
:tmp_path => "/tmp"                   # path where temporary files will be stored
}

{% endhighlight %}


After Setting Java path , classpath separator and tmp path now do following step.

<br />

{% highlight ruby %}
class PdfController < ActionController::Base
  acts_as_flying_saucer

  def generate_pdf
    render_pdf :template => 'pdf/pdf_template'
  end
end
  render_pdf :file=>'pdf/generate_pdf.html.erb'
  render_pdf :template=>'pdf/generate_pdf.pdf.erb',
             :send_file => { :filename => 'pdfdoc.pdf' }
{% endhighlight %}

<br />

Add act_as_flying_saucer to controller then render_pdf.


There are various ways to render pdf using "<strong>template</strong>" or "<strong>file</strong>",<strong>:send_file</strong> option use to send pdf file to client side.if we are using any <strong>external css</strong> file then this css shoulda have <strong>medi</strong>a option as<strong> 'print'</strong>.

<br />

{% highlight ruby %}

<%= stylesheet_link_tag 'pdf' ,:media=>'print' %>

{% endhighlight %}

If pdf containing images which generate on the fly.so instead of using

<br />

{% highlight ruby %}<%= image_tag %>{% endhighlight %}


use


{% highlight html %} <img src=" " >{% endhighlight %}

Before rendering PDF validate HTML,like whether all tags are close properly or not.otherwise it gives an parse error.

<br />

Now You are ready to Generate PDF. Hurray!!!!!!!!!

<br />

How to generate Header, Footer,Page Number and Automation Of HTML Validation will be discussed in next post.

<br />
