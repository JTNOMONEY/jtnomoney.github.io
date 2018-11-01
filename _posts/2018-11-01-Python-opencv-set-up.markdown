---
layout: post
title:  "Install Python and OpenCV on windows"
date:   2018-11-01 12:23:10 +0800
categories: git
---

My friend was asking me how to set up python environment since he had tried for a while but failed on his windows based enviroment.
I have few experience though and all of the experence is based on Linux system. All I can recall are about the embedded porting for SAMBA application 
in which some codes relates to python and some material for cross-toolchain that scripts in python. So I spend some time to reference open course[1]

Here I note the steps for someone who needs as reference as well as for my friend. 

Install Anaconda
---
Anaconda is a good start for rookie (like me) to prement of conflictions on package installations. We can find the latest one on https://www.anaconda.com/download/ and just clicking "next step" until installation sucessfully.After installation, we can open Anaconda Prompt with admin user.

Check the conda version 
{% highlight shell %}
conda --version
# conda 4.5.11
{% endhighlight %}

Under Anaconda Prompt, create an enviornment which is based on python 3.5.2.
{% highlight shell %}
conda create -n opencv_py352_demo python=3.5.2
{% endhighlight %}

Check one of env you created, naming opencv_py352_demo
{% highlight shell %}
conda info --envs
# conda environments:
#
base                     C:\ProgramData\Anaconda3
opencv_py352_demo     *  C:\ProgramData\Anaconda3\envs\opencv_py352_demo
{% endhighlight %}

If you want to check all envs. and remove some of them, you can type:
{% highlight shell %}
conda remove --name myenv --all
conda env remove --name myenv
{% endhighlight %}

Install OpenCV
---

OpenCV, Spyder, SciPy and matplotlib

Spyder editor is strong IDE tools, and looks likes MATLAB env. If you are going to learn OpenCV, SciPy (pronounced “Sigh Pie”) and matplotlib are good combinations to do simulations on mathematics, science, engineering applications.

Install OpenCV
{% highlight shell %}
conda install -c https://conda.anaconda.org/menpo opencv3
{% endhighlight %}

Install spyder
{% highlight shell %}
conda install spyder
{% endhighlight %}

Install matplotlib
{% highlight shell %}
conda install matplotlib
{% endhighlight %}

Open spyder IDE
{% highlight shell %}
spyder
{% endhighlight %}

Run an example on my environment [2]
![pic01](/media/images/spyder_python.png)

Reference
---
[1] http://cs231n.github.io/python-numpy-tutorial/

[2] https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_gradients/py_gradients.html#gradients


