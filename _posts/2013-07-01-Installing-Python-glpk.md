---
layout: post
title: "Installing python-glpk on OS X 10.8"
date: 2013-07-01 11:00
disqus: y
categories: python
---
I have been using [PuLP](https://code.google.com/p/pulp-or/) for linear optimisation. By default, on OS X, the library used the packaged [COIN](http://www.coin-or.org/) command line program. This tends to be slow if you are many optimisations as I was doing. Luckily PuLP can handle other optimisers as well like [GLPK](http://www.gnu.org/software/glpk/glpk.html) or paid ones like [CPLEX](http://www.cplex.com/) or [GUROBI](http://www.gurobi.com/).

So I decided to install GLPK on my computer. This proved harded than I initially imagined.

Installing GLPK assuming [Homebrew](http://brew.sh/) is installed:

{% highlight bash %}
brew install homebrew/science/glpk
{% endhighlight %}

Now to install python bindings for GLPK. I tried out two binding for python (more details [here](http://en.wikibooks.org/wiki/GLPK/Python)):

* Python-GLPK
* PyGLPK

I didn't have any success with PyGLPK. So I stuck with Python-GLPK.

My instructions:

{% highlight bash %}
wget http://www.dcc.fc.up.pt/~jpp/code/python-glpk/python-glpk_0.4.43.orig.tar.gz
tar xf python-glpk_0.4.43.orig.tar.gz
cd python-glpk-0.4.43/src/
{% endhighlight %}

In swig/Makefile replace line number to
{% highlight bash%}
PYVERS := 'python2.7'
{% endhighlight %}

In folder 'src', run
{% highlight bash%}
make
{% endhighlight %}

Ignore any errors. Now run:

{% highlight bash%}
cp swig/glpkpi.py python/glpkpi.py
python setup.py install
{% endhighlight %}

This should install the library. To test if the install worked, go to the examples directory

{% highlight bash%}
cd ../examples
python test.py
{% endhighlight %}
