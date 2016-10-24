---
title:  "Welcome!"
date:   2016-07-01 18:00:00
categories: [blog]
tags: [blog]

excerpt: Welcome to the bastion of the damned
---

Welcome to my blog!

Stay tuned for updates on my personal projects and general thoughts and musings.

See you soon!

{% highlight apache %}
<Virtualhost *:80>
	ServerName WWW.YOURAPP.COM
	ServerAlias YOURAPP

	WSGIDaemonProcess YOURAPP user=YOU group=YOU threads=5 home=/PATH/TO/YOURAPP/
	WSGIScriptAlias / /PATH/TO/YOURAPP/YOURAPP.wsgi

	<Directory /PATH/TO/YOUR/APP>
		WSGIProcessGroup YOURAPP
		WSGIApplicationGroup %{GLOBAL}
		WSGIScriptReloading On
		Order deny,allow
		Allow from all
	</Directory>
</Virtualhost>
{% endhighlight %}
