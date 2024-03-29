# Quick-PyPI

The simplest and quickest way to build and publish a PyPI package

## Installation
```pip
pip install quick-pypi
```

## Minimum Example

Before you start, you need to have several things:
- Determine a unique PyPI package name, easy to remember, like 'quick-pypi-test';
- Have a PyPI account, then export your upload token to a txt file in your computer;
- Use PyCharm IDE or VSCode to develop your own package. We support Jupyter Notebook now!

Step 1: Prepare your project tree like:
```
Project Root
 -- src
   -- your_package_name
     -- __init__.py
     -- your_class.py   # where you can write your own code!
 -- dists               # auto generated folder storing uploading version history
   -- 0.0.1
   -- 0.0.2
   -- ...
   -- VERSION           # a file storing the latest version of uploading
 quick_pypi.py          # Main settings of uploading package
```

Step 2: The simplest `quick_pypi.py` file content is below: 
```python
from quick_pypi.deploy import *
auto_deploy(
    cwd=os.path.dirname(os.path.realpath(__file__)), # When using jupyter notebook, using `cwd=os.getcwd()`
    name="quick-pypi-test",
    description="This is a quick-pypi-test package!",
    pypi_token='../../pypi_upload_token.txt', # the token string or path from your PyPI account
)
```

Step 3: Deploy the package to PyPI server

After you finish writing your codes in the `src` package, you can just simply right-click the `quick-pypi.py` to run, and wait for its completion.

Step 4: Check if the package is uploaded successfully!

## Complicated Example settings for advanced users

A real example is here:

```python
from quick_pypi.deploy import *
# or you can use: `from quick_pypi.deploy_toml import *`

auto_deploy(
    cwd=os.path.dirname(os.path.realpath(__file__)),
    name="pyrefworks",
    long_name="A Python Toolkit for RefWorks Data Analysis",
    description="Converting RefWorks files into a CSV table file",
    long_description="This is a project to convert RefWork files to a CSV file",
    src_root="src",
    dists_root=f"dists",
    pypi_token='../pypi_upload_token.txt', # a file storing the token from your PyPI account
    test=False, # determine if uploading to test.pypi.org
    version="0.0.1a0", # fixed version when uploading or using version='auto'
    project_url="http://github.com/dhchenx/pyrefworks",
    author_name="Donghua Chen",
    author_email="xxx@xxx.com",
    requires="quick-csv",
    license='MIT',
    license_filename='LICENSE',
    keywords="refworks, csv file",
    github_username="dhchenx",
    max_number_micro=20, # major.minor.micro
    max_number_minor=20, # version maximum numbers in each part, e.g. 0.0.20 --> 0.1.0; 0.20.20 --> 1.0.0
    # only_build=True
)
```
Here you can provide more information about your package, like setting your author's name, email, license, short or long names and descriptions, etc. 

### Deploy to local computer without upload

```python
import quick_pypi as qp

qp.deploy(
    src_root="src",
    dist_root='data/dist1',
   # name="quick-pypi-test",
   # description="This is a quick-pypi project",
    version="0.0.1a0", # fixed version number, wont change
   # project_url="http://github.com/dhchenx/quick-pypi-test",
   #  author_name="Donghua Chen",
    # author_email="douglaschan@126.com",
    # requires="jieba;quick-crawler",
    # license='MIT',
    # license_filename='LICENSE'

)
```
This will generate a series of actual package files (e.g. README.md, LICENSE,setup.py, etc. ).

Then, you can manually build the package through twine in the directory of `dist1`. 

An example using our toolkit to deploy in the PyPI platform is demonstrated [here](https://pypi.org/project/pyrefworks/).

## License
The `quick-pypi` project is provided by [Donghua Chen](https://github.com/dhchenx). 

