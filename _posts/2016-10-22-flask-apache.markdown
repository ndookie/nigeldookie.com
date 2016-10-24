---
title:  "The thing about Flask and Apache"
date:   2016-10-22 00:00:00
categories: [blog]
tags: [blog]


excerpt: Steps for deploying a Flask application using an Apache webserver 
---

In the building of [shrten.me][shorten], I eventually had to make a decision as to how I plan on hosting this web app. 

Many platforms offer an easy mechanism for hosting a Flask app, such as [Heroku][heroku] and [Google App Engine][google_engine], but alas, those choices were not for me.

In the pursuit of understanding the intricacies of hosting, I decided to host the app on my VM using Apache, but all was not well. 

It's astounding the amount of different solutions presented online for this problem, and how few of them seem to work for me. Here I will describe my WSGI file and Apache config file for those who may be in the same position as me.

Instances of YOURAPP must be replaced with, obviously, your app!

{% highlight ruby %}
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

The WSGI file, while simple, isn't well described in most articles. This worked for me.


{% highlight python %}
import sys

sys.path.append('/PATH/TO/YOURAPP')

from YOURAPP import app as application
{% endhighlight %}

When that's all said and done, enable your site, and reboot apache!

{% highlight ruby %}
sudo a2ensite YOURAPP
sudo service apache2 restart
{% endhighlight %}

If you have any questions feel free to hit me an [email][email] with your problem!.

Cheers!

[heroku]: http://heroku.com
[google_engine]: https://cloud.google.com/appengine/docs
[email]: mailto:ndookie@gmail.com
[shorten]: http://shrten.me