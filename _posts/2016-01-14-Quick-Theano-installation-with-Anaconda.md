---
layout: post
category : 
tagline: ""
tags : [Theano, Anaconda, Installation]
---
{% include JB/setup %}

This describes a quick way of installing Theano on a Windows machine, based on the [official general instructions](http://deeplearning.net/software/theano/install.html).

1. Install the latest python with numpy, pip package manager, etc. by installing [AnacondaCE](https://www.continuum.io/downloads). Note: at the time of writing, Anaconda PYTHON 3.5 is not stable on Windows due to missing build of libpython in condo that's compatible with Python 3.5. I recommend installing Anaconda Python 2.7.

1. Once installed, run the following in Anaconda Prompt 

        conda install mingw libpython

1. Create a directory where you want to enlist Theano source code and run

        git clone git://github.com/Theano/Theano.git
        cd Theano
        python setup.py develop
        
1. Verify that Theano is properly installed by 
        
        import theano

1. Create $HOME$ system variable and place ```.theanorc.txt``` Theano config file inside the folder that $HOME$ points to. 

Test mathjax: $x^2 + 2b$
