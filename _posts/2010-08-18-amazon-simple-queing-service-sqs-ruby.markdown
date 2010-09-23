--- 
wordpress_id: 230
layout: default
title: Amazon Simple Queing Service (SQS) + Ruby
wordpress_url: http://railstech.com/?p=230
---
<h1 class="page-title">{{ page.title }}</h1>
<span class="author">Author :- Virendra Negi </span>
<br />
<hr />

Amazon SQS is a distributed queue messaging service. The idea of SQS is to remove the direct associations between producer and consumer and act as mediator between them.
<br />
Consider that you have a large application like websites monitoring which involve many stages like
<ul>
	<li>Downloading a website</li>
	<li>Processing the downloaded website</li>
	<li>Generating report of the above processing</li>
</ul>
So instead of clubbing the above three one can just split them on their specific need(based on the work they do) with each doing their respective task and on completion notify the other about it completion.
<br />

The traditional approach (called as <a title="Client-Server railstech" href="http://en.wikipedia.org/wiki/Clientserver_model" target="_blank">Client-Server</a> architecture) is to send the notification using a simple <a title="HTTP railstech" href="http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol" target="_blank">HTTP</a> ,<a title="REST railstech" href="http://en.wikipedia.org/wiki/Representational_State_Transfer" target="_blank">REST</a> , <a title="SOAP railstech" href="http://en.wikipedia.org/wiki/SOAP" target="_blank">SOAP</a> etc request. But it too has some disadvantage as it require extra care and precision to handle all possible response e.g Time-out,Server down etc.

One can save this time and effort my using SQS.

e.g Instead of sending the direct request to Server one can use to SQS to interact with Server/Client an can eventually cut down some of drawback of traditional architecture.

Setting up Amazon SQS in <a title="Ruby railstech" href="http://www.ruby-lang.org/en/" target="_blank">Ruby</a>: There are various library available for using Amazon SQS in Ruby (e.g <a title="right_aws SQS railstech" href="http://github.com/rightscale/right_aws" target="_blank">right_aws</a>, <a title="SQS gem railstech" href="http://github.com/qoobaa/sqs" target="_blank">sqs</a>)

<strong>Pre-requitise:</strong>
<ul>
	<li>aws-access-key-id</li>
	<li>aws-secret-access-key</li>
	<li>ruby-library(<a title="right_aws  railstech.com" href="http://github.com/rightscale/right_aws" target="_blank">right_aws</a> or <a title="SQS gem railstech" href="http://github.com/qoobaa/sqs" target="_blank">sqs</a> gem)
both of which is provide by the Amazon (or you can ask for incase) during the process of account-registration</li>
</ul>
In your <strong>irb</strong> console
{% highlight ruby %}
require "rubygems"

require "right_aws"

aws_access_key_id = "Your access key id"

aws_secret_access_key = "Your secret access Key"

sqs = RightAws::SqsGen2.new(aws_access_key_id,aws_secret_access_key)
{% endhighlight %}
This basically initialize the sqs object for you to work on.
<br />
One can create a new queue just by a single method.

{% highlight ruby %} queue(queue_name, create=true, visibility=nil) {% endhighlight %}

carefully look at parameter supplied.

<blockquote>
<em>
queue_name => name of queue.

create => true (create a queue if it does not exist (optional)).

visibility => set visibility (which make the message reappear after a specified time if not delete from queue).
</em>
</blockquote>

<br />
One key point about visibility is that one can't set visibility more than 7200 sec for a queue or a message .But you can set so from <a title="RightScale railstech" href="http://www.rightscale.com/" target="_blank">RightScale</a> (<strong>Cloud Computing management Platform</strong>).

e.g
{% highlight ruby %}
my_queue = queue('queue_1')
{% endhighlight %}
just look at few other methods.

1 <strong>send_message</strong> or <strong>push</strong> :- Send message to the specified queue.
{% highlight ruby %}
 my_queue.send_message "This is my first message"
{% endhighlight %}

2 <strong>receive</strong> or <strong>pop</strong> :- Receive message from the specified queue.
{% highlight ruby %}
 message_received = my_queue.receive

puts message_received.body
=>; "This is my first message";
{% endhighlight %}
<br />
3 <strong>receive_messages</strong> : - There is also a method called receive_messages to receive an array of messages but it never returned me more than one message so if it work for you it fine then syntax is like this

{% highlight ruby %}
 receive_messages(number_of_message=1,visibility=nil)

 my_queue.receive_messages(2,60) => return and array of messages
{% endhighlight %}
<br />
4 <strong>delete </strong>: - Delete a message or a queue

{% highlight ruby %}
 my_queue.delete => "delete the my_queue for SQS"

 message_received.delete => "delete the message from the intended queue"
{% endhighlight %}
<br />
5 <strong>size</strong> :- Specify the no of message in?the queue

{% highlight ruby %}
 my_queue.size => 4 #"4" message in my_queue
{% endhighlight %}
<br />

6 <strong>name</strong> :- Specify name of the queue

{% highlight ruby %}
 my_queue.name => "queue_1" #Name of the queue
{% endhighlight %}
<br />

Note  There is delay lag in all request and response sent or received to or from SQS server don't assume to work it instantaneous approximately of around 45 sec -1 minute or it can be more.

<em>e.g </em>

If you send a message to the queue don't assume it to appear instantaneously in the queue
<br />
<strong>Pricing Model </strong> => $0.10 per 100,000 requests.

 Message Size   => 64KB

<br />

<em>For more information on Pricing and message size click <a title="AMAZON SQS railstech" href="http://aws.amazon.com/about-aws/whats-new/2010/07/01/amazon-sqs-introduces-free-tier-and-adds-support-for-larger-messages-and-longer-retention/" target="_blank">here</a>.</em>

Thank you

<br />
