---
title: The World of Python Libraries
description: >
  A talk given at a HacSoc meeting in conjunction with Jeff Copeland.  Jeff gave
  an introduction to Python, and this 15-minute presentation gives an overview
  of the world of Python packages, the source of Python's power.
layout: presentation
---

{{site.startslide}}

# The World of Python Libraries

HacSoc 9/9/15

Stephen Brennan

{{site.nextslide}}

## Now that you know Python ...

... how do you make something exciting?

By using <del>other people's code</del> <ins>libraries</ins>!

This is a guide to Python's libraries.

Don't take notes, my slides are at:

<http://stephen-brennan.com/talks>.

{{site.nextslide}}

## The best Python libraries are ...

... the standard libraries!

- Useful basics:
  [`collections`](https://docs.python.org/3/library/collections.html),
  [`re`](https://docs.python.org/3/library/re.html),
  [`random`](https://docs.python.org/3/library/random.html),
  [`argparse`](https://docs.python.org/3/library/argparse.html),
  [`logging`](https://docs.python.org/3/library/logging.html),
  [`pprint`](https://docs.python.org/3/library/pprint.html),
  [`unittest`](https://docs.python.org/3/library/unittest.html).
- Basic networking: [`socket`](https://docs.python.org/3/library/socket.html).
- Reading/writing data:
  [`pickle`](https://docs.python.org/3/library/pickle.html),
  [`csv`](https://docs.python.org/3/library/csv.html),
  [`json`](https://docs.python.org/3/library/json.html).
- Concurrency: [`threading`](https://docs.python.org/3/library/threading.html),
  [`multiprocessing`](https://docs.python.org/3/library/collections.html).
- High-level: [`itertools`](https://docs.python.org/3/library/itertools.html),
  [`functools`](https://docs.python.org/3/library/functools.html).
- Utility: [`os`](https://docs.python.org/3/library/os.html),
  [`sys`](https://docs.python.org/3/library/sys.html),
  [`subprocess`](https://docs.python.org/3/library/subprocess.html).
- See the full list [here](https://docs.python.org/3/library/index.html).

{{site.nextslide}}

## Crash course in Python packaging

- TL;DR: `pip install package-name`
- Some packages need to be compiled first!
    - Read their documentation about how to install.
    - Windows users: check [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/)
      for pre-built binaries.
    - Linux users: your package manager may have binaries.
- If you don't have root, try `pip install --user package-name`.
- Or, check out [Virtualenv](https://virtualenv.readthedocs.org/en/latest/).

{{site.nextslide}}

## Web development frameworks

- [Django](https://www.djangoproject.com/) - widespread MVC framework, used by
  Instagram, Pinterest, Disqus, Bitbucket, ...
- [Flask](http://flask.pocoo.org/) - small "micro-framework" for simple apps.
- [Tornado](http://www.tornadoweb.org/en/stable/) - scalable, non-blocking
  networking library that works well for web dev
- Other common names: [Pyramid](http://www.pylonsproject.org/), Zope, Web.py

{{site.nextslide}}

## Web development tools

- [Jinja2](http://jinja.pocoo.org/) - simple templating system for HTML (or any
  other text file)
- [MarkupSafe](http://www.pocoo.org/projects/markupsafe/) - HTML escaping!

{{site.nextslide}}

## Databases

- [Psycopg2](http://initd.org/psycopg/) - interface to PostgreSQL
- [sqlite3](https://docs.python.org/3/library/sqlite3.html) - standard library
  interface for small databases in local files
- [SQLAlchemy](http://www.sqlalchemy.org/) - widely used "database abstraction
  layer" used by Dropbox, Hulu, reddit, Yelp, Uber, ...
- Django has a good built-in database abstraction layer, too.

{{site.nextslide}}

## Web scraping

- [Requests](http://docs.python-requests.org/en/latest/) - the **easiest** way
  to make HTTP requests (e.g. download web pages).  Used by Amazon, Google,
  Twitter, Mozilla, PayPal, ...
- [lxml](http://lxml.de/) - parser for HTML and XML.  *Fast,* because it uses C
  libraries to do the heavy lifting
- [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/) - "parser" for
  *badly written* HTML.
- [Scrapy](http://scrapy.org/) - web scraping "framework" that lends itself to
  making crawlers.  Python 2 only :(

{{site.nextslide}}

## Testing

- [Nose](https://nose.readthedocs.org/en/latest/#) - unit test runner that
  extends the standard library.
- [Coverage](http://nedbatchelder.com/code/coverage/) - measure code coverage of
  your tests
- [Tox](http://tox.readthedocs.org/en/latest/) - automated framework for testing
  on multiple Python versions and environments
- [factory_boy](https://factoryboy.readthedocs.org/en/latest/) - automatically
  generate valid objects to make testing easier

{{site.nextslide}}

## Scientific

Python is one of the best ecosystems for doing scientific and numerical
computing.  Its advantage over specialized systems (Mathematica, Octave, Matlab)
is its wide range of general programming libraries to complement the specialized
scientific libraries.  You'll find it is a strong contender if you do any sort
of research that involves numerical computing.

{{site.nextslide}}

## Scientific Python Stack

- [NumPy](http://www.numpy.org/) - efficient numerical computations with
  vectors, matrices, and other multidimensional arrays
- [SciPy](http://www.scipy.org/) - scientific algorithms (clustering,
  integration, linear algebra, etc)
- [Pandas](http://pandas.pydata.org/) - extends NumPy data structures with data
  labels, advanced manipulation, broadcasting, slicing, querying, and I/O.
- [Matplotlib](http://matplotlib.org/) - plotting library for producing
  professional figures
- [IPython](http://www.ipython.org) - feature-rich interactive console and
  "notebook" for doing scientific computing and viewing results
- [SymPy](http://www.sympy.org/en/index.html) - Python computer algebra system

{{site.nextslide}}

## More Science

- [scikit-learn](http://scikit-learn.org/stable/) - provides simple and
  efficient machine learning algorithms
- [NetworkX](http://networkx.github.io/) - graph library that provides standard
  algorithms, analysis tools, etc.
- [NLTK](http://www.nltk.org) - a natural language processing library
- [Caffe](http://caffe.berkeleyvision.org/) - "deep learning" framework with a
  Python interface
    - Used by Google to create Deep Dream images
    - **Very difficult to install.**

{{site.nextslide}}

## Utilities

- [Colorama](https://pypi.python.org/pypi/colorama) - cross platform colored
  terminal output
- [Pygments](http://pygments.org/) - syntax highlighter, very useful for
  code-related websites
- [Netaddr](https://pythonhosted.org/netaddr/) - "library for representing and
  manipulating network addresses" such as IP addresses and CIDR ranges
- [Pillow](https://pypi.python.org/pypi/Pillow/2.0.0) - Python imaging library
- [PyCrypto](https://www.dlitz.net/software/pycrypto/) - Never roll your own
  crypto.

{{site.nextslide}}

## Automation

- [Selenium](http://docs.seleniumhq.org/) - library for automating web browsers
- [Ansible](http://www.ansible.com/home), [Fabric](http://www.fabfile.org/),
  [SaltStack](http://saltstack.com/) - all different approaches to remotely
  managing lots of computers (like servers)
    - Fabric is a good way to start for deploying your web app!

{{site.nextslide}}

## Miscellaneous

- [redis](https://pypi.python.org/pypi/redis/) - Redis is a key-value database.
  You can use it from Python with this client.
- [Celery](http://www.celeryproject.org/) - A task queue library.  Useful for
  offloading heavy computation from web servers onto other machines.
- [PyParsing](https://pypi.python.org/pypi/pyparsing/2.0.3) - Simple tool for
  creating and parsing grammars.
- [PLY](http://www.dabeaz.com/ply/) - more powerful tool for parsing grammars,
  preferred by Tim Henderson.
- [PyGame](http://pygame.org/news.html) - Library for making games in Python.

{{site.nextslide}}

## Documentation

- If you ever write your own library that's anything more than a couple
  functions, you need documentation.
- [Sphinx](http://sphinx-doc.org/) is the best tool for creating documentation
  for Python libraries.
- Creates pretty documentation like
  [this](http://factoryboy.readthedocs.org/en/latest/).
- It can be used with C and C++, or to write any non-code related documentation.

{{site.nextslide}}

## Conclusion

- Whenever you need to do something in Python, spend 5 minutes perusing the
  standard library.  You may turn something up!
- You can almost always turn up a useful Python library with a quick Google
  search.
- You'll find strong support for research, web development, web scraping, and
  automating simple tasks.
- Try picking a couple Python libraries and see how you can combine them!

{{site.endslide}}
