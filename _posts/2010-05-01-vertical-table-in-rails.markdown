--- 
wordpress_id: 112
layout: default
title: Vertical table in rails
wordpress_url: http://railstech.com/?p=112
---
{% include post-nav.textile %}
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Amar Daxini </span>
<br />
<hr />
In this article i have just taken a short example describing <strong>vertical table</strong>,and its implementation  using rails.

When table has no fixed column it has dynamic fields .data is not stored  on separate column but <strong>data stores in vertical fashion</strong>.

For implementing vertical table table has mainly <strong>2 columns key and value </strong>pair<strong>.key</strong> is like database<strong> column </strong>name and <strong>value</strong> contains actual <strong>data</strong>.

<br />

Lets take an e.g

Consider website in which it contains various products and its comparison ,searching  and many more features.product can be mobile,car etc.Product has many items.item may be nokia 6600,nokia n72 etc.

Here our aim is not compare aur search items.Here our main aim is how vertical table concept is applied.Suppose we have to build only single product comparison site then each product has it's own attributes that can be easily build with adding column for each product.

we are developing generic site like multiple product,so there is no fixed attributes,each product has it's own attributes either we create different model for each product or we can proceed with vertical table concept.

<img class="size-full alignnone" title="Vertical table" src="/images/posts/model.jpeg" alt="Vertical table" />
<ul>
	<li>Product has many Product Attributes.</li>
	<li>Product has many Items.</li>
	<li>Item has many Item Attributes.</li>
	<li>Item Attribute belongs to Product Attribute.</li>
</ul>
**Product Attribute mainly requires 3 fields**

**name  :** which is used for key in vertical table i.e column name

<br />

**option_type :** which is used for viewing different form of data when item is created like text box, drop down,checkbox,multi option

<br />

**option :** which contain option if its drop down or multi option i.e serialize.

<br />

**Item has only name field which is optional**

<br />

**Item attribute mainly required 3 fields**

<br />

**name :** key name or column name

<br />

**value :** actual value

<br />

**item_id :** foreign key of item

It is used where table has **dynamic fields** , and it only concern with data.

Here **data** grows **vertically**.

<br />
It has mainly key ,value  pair.

Source code of above example is hosted on github <a href="http://github.com/amardaxini/vertical_table_demo">http://github.com/amardaxini/vertical_table_demo</a>

For More info about vertical table you can visit <a href="http://weblogs.foxite.com/andykramek/archive/2009/05/03/8369.aspx">http://weblogs.foxite.com/andykramek/archive/2009/05/03/8369.aspx</a>

