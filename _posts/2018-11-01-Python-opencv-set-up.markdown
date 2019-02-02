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
Anaconda is a good start for rookie (like me) to avoid some conflictions on package installations. We can find the latest one on [Anaconda](https://www.anaconda.com/download/) and just clicking "next step" until installation sucessfully.After installation, we can open `Anaconda Prompt` with admin user.

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

If you have generated opencv_py352_demo, you can activate directly
{% highlight shell %}
activate opencv_py352_demo
{% endhighlight %}

Install OpenCV
---

OpenCV, Spyder, SciPy and matplotlib

Spyder editor is strong IDE tools, and looks likes MATLAB env. If you are going to learn OpenCV, SciPy (pronounced “Sigh Pie”) and matplotlib are good combinations to do simulations on mathematics, science, engineering applications.

Install OpenCV
{% highlight shell %}
conda install -c https://conda.anaconda.org/menpo opencv3
conda install -c conda-forge opencv
{% endhighlight %}

Install spyder
{% highlight shell %}
conda install spyder
{% endhighlight %}

Install matplotlib
{% highlight shell %}
conda install matplotlib
{% endhighlight %}

Check all installed package
{% highlight shell %}
conda list
# packages in environment at C:\ProgramData\Anaconda3\envs\opencv_py352_demo:
#
# Name                    Version                   Build  Channel
alabaster                 0.7.11                   py35_0
asn1crypto                0.24.0                   py35_0
astroid                   2.0.4                    py35_0
babel                     2.6.0                    py35_0
backcall                  0.1.0                    py35_0
blas                      1.0                         mkl
bleach                    2.1.4                    py35_0
ca-certificates           2018.03.07                    0
certifi                   2018.8.24                py35_1
cffi                      1.11.5           py35h74b6da3_1
chardet                   3.0.4                    py35_1
cloudpickle               0.5.5                    py35_0
colorama                  0.3.9            py35h32a752f_0
cryptography              2.3.1            py35h74b6da3_0
cycler                    0.10.0           py35hcc71164_0
decorator                 4.3.0                    py35_0
docutils                  0.14             py35h8ccb97f_0
entrypoints               0.2.3                    py35_2
freetype                  2.9.1                ha9979f8_1
html5lib                  1.0.1                    py35_0
icc_rt                    2017.0.4             h97af966_0
icu                       58.2                 ha66f8fd_1
idna                      2.7                      py35_0
imagesize                 1.1.0                    py35_0
intel-openmp              2019.0                      118
ipykernel                 4.10.0                   py35_0
ipython                   6.5.0                    py35_0
ipython_genutils          0.2.0            py35ha709e79_0
isort                     4.3.4                    py35_0
jedi                      0.12.1                   py35_0
jinja2                    2.10                     py35_0
jpeg                      9b                   hb83a4c4_2
jsonschema                2.6.0            py35h27d56d3_0
jupyter_client            5.2.3                    py35_0
jupyter_core              4.4.0                    py35_0
keyring                   13.2.1                   py35_0
kiwisolver                1.0.1            py35h6538335_0
lazy-object-proxy         1.3.1            py35hfa6e2cd_2
libpng                    1.6.34               h79bbb47_0
libsodium                 1.0.16               h9d3ae62_0
markupsafe                1.0              py35hfa6e2cd_1
matplotlib                3.0.0            py35hd159220_0
mccabe                    0.6.1                    py35_1
mistune                   0.8.3            py35hfa6e2cd_1
mkl                       2019.0                      118
mkl_fft                   1.0.6            py35hdbbee80_0
mkl_random                1.0.1            py35h77b88f5_1
nbconvert                 5.3.1                    py35_0
nbformat                  4.4.0            py35h908c9d9_0
numpy                     1.15.2           py35ha559c80_0
numpy-base                1.15.2           py35h8128ebf_0
numpydoc                  0.8.0                    py35_0
opencv3                   3.1.0                    py35_0    menpo
openssl                   1.0.2p               hfa6e2cd_0
packaging                 17.1                     py35_0
pandoc                    2.2.3.2                       0
pandocfilters             1.4.2                    py35_1
parso                     0.3.1                    py35_0
pickleshare               0.7.4            py35h2f9f535_0
pip                       10.0.1                   py35_0
prompt_toolkit            1.0.15           py35h89c7cb4_0
psutil                    5.4.7            py35hfa6e2cd_0
pycodestyle               2.4.0                    py35_0
pycparser                 2.19                     py35_0
pyflakes                  2.0.0                    py35_0
pygments                  2.2.0            py35h24c0941_0
pylint                    2.1.1                    py35_0
pyopenssl                 18.0.0                   py35_0
pyparsing                 2.2.1                    py35_0
pyqt                      5.9.2            py35h6538335_2
pysocks                   1.6.8                    py35_0
python                    3.5.2                         0
python-dateutil           2.7.3                    py35_0
pytz                      2018.5                   py35_0
pywin32                   223              py35hfa6e2cd_1
pyzmq                     17.1.2           py35hfa6e2cd_0
qt                        5.9.6            vc14h62aca36_0
qtawesome                 0.4.4            py35h639d0ff_0
qtconsole                 4.4.1                    py35_0
qtpy                      1.5.0                    py35_0
requests                  2.19.1                   py35_0
rope                      0.11.0                   py35_0
setuptools                40.2.0                   py35_0
simplegeneric             0.8.1                    py35_2
sip                       4.19.8           py35h6538335_0
six                       1.11.0                   py35_1
snowballstemmer           1.2.1            py35h4c55bfa_0
sphinx                    1.7.9                    py35_0
sphinxcontrib             1.0                      py35_1
sphinxcontrib-websupport  1.1.0                    py35_1
spyder                    3.3.1                    py35_1
spyder-kernels            0.2.6                    py35_0
sqlite                    3.25.2               hfa6e2cd_0
testpath                  0.3.1            py35h06cf69e_0
tornado                   5.1.1            py35hfa6e2cd_0
traitlets                 4.3.2            py35h09b975b_0
typed-ast                 1.1.0            py35hfa6e2cd_0
urllib3                   1.23                     py35_0
vc                        14                   h0510ff6_3
vs2015_runtime            14.15.26706          h3a45250_0
wcwidth                   0.1.7            py35h6e80d8a_0
webencodings              0.5.1                    py35_1
wheel                     0.31.1                   py35_0
win_inet_pton             1.0.1                    py35_1
win_unicode_console       0.5              py35h56988b5_0
wincertstore              0.2              py35hfebbdb8_0
wrapt                     1.10.11          py35hfa6e2cd_2
zeromq                    4.2.5                he025d50_1
zlib                      1.2.11               h8395fce_2
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


