# Swiss Python Summit 2016
## Python Guide to the Galaxy
- https://github.com/tomron
- Code samples: https://github.com/tomron/python_swiss_2016

### Data Structures
#### Collections
- namedtuple() / slots
- deque: prev/next item
- Counter
	- _defaultdict for integer_
	- + operand implemented
- OrderedDict
- defaultdict

#### itertools
- Infinte iterators
	- count, cycle, repeat
- Iterators terminting on the shortes input sequence
- 3rd?

combintations
permutations
groupby

### Dates
- `time`, based on epoch time
- `datetime`, includes tz
	- `timedelta`
		- `.seconds` vs `.total_seconds`
- `calendar`

### Text
#### Unicode

	@ -*- coding: uft-8 -*-
	len('ü') -> 2
    len(u'ü') -> 1
	len(u'ü'.encode('utf-8)) -> 2
	len(u'ü'.encode('latin1)) -> 1

#### Regex
    re.findall(regex, sentence) -> results
    re.match() / match.groups() .group() .span()
    re.search() / .groupdict() named regex parameters

## API Design is Hard
- https://github.com/davehalter
- https://twitter.com/jedidjah_ch

### Jedi and jedi-vim
- autocompletions (if you don't use PyCharms)

### Interesting Talks
- API Design: Lessons Learned by Raimond Hettinger (not the one on Youtube)
- Good API Design by Alex Martelli

### Writing Code
- Testing: py.test & tox
- Documentation: sphinx

### API
- Interfaces in Python: `abc.ABCMeta`

#### Bad APIs
- No API
- One way to use the API, and only one
- Inconsistency / Java-style `getMember()` (PEP-8)

#### Designing an API
- Data types
- Don't do IO that is not readable by other languages, like `pickle`
- Performance: `async` in Python 3.5

#### Private/Protected/Public
- `_variable` for protected
- `__variable` for private (don't use a lot)
- Use `_` a lot

#### Naming
- Nouns are for attributes
- verbs are for methods, but not like get_foo()
- Example `requests` module
	- `r.text`
	- `r.json()` why???

#### Named Arguments
	twitter_search('python', num_results=3, retweets=False)

For Python 3 use the `*` argument

	def twitter_search(..., *, num_results, retweets)

#### Properties
Use them, but only for clear defined "getters":

	@property
    def line_nr(self):
    	return 42

Interface of property cannot be changed, compared to:

	def do_something(self):
    def do_something(self, new_option=False)

#### Transitions
- Incremental transitions
- Deprecate with warnings & documentation
	- `warnings.warn('Use name instead.', DeprecationWarning)`
- Start interpreter with `$ python -Wall`

## CFFI - Calling C from Python
Armin Rigo
- pypi-ranking.info

### CFFI

"Call C from Python"
C Foreign Function Interfaces

https://cffi.readthedocs.org

Works also on PyPy because it generates Python code


#### Howto

	$ man getpwuid
    import cffi
    ffi = cffi.FFI()
    ffi = cdef("""
    	<copy and paste the code from the man page>
    """)
    ffi.set_source("so file", """
    	#includes
        ...
    """)
    ffi.compile

	$ python that_file.py
	==> _pwuid_cffi.so was compiled

    from _pwuid_cffi import lib, ffi

### PyPy
- Prompt: `>>>>`
- Goal: performance
- Works great for Python code, not so easy to work with C extensions.
	- Use cases: Django, etc.
    - For C extensions look into the module `~cext`

## 3D CG with Python
Martin Christen
Slides: http://www.slideshare.net/martinchristen/3d-computer-graphics-with-python

### Blender
Open Source 3D creation suite ("more than modelling"):
incl. animation, video editing, games and Python scripting

#### Module
`bpy.data`

	list(bpy.data.objects)

Open the console in Blender, it shows the Python code for every modification that is done. The easiest way to learn it.

### Low Level 3D Application

Open GL
https://pyopengl.sourceforce.net

DirectPython 11: Drrect3D 11 (Windows-only)
http://directpython11.sourceforge.net

#### OpenGL
Many compatible GUI toolkit.
- pyglet => easier than Qt to install

Primitives are converted to Fragmants (Pixels) (projected to the screen).
- Vertrex-Operations
- Framgent-Operations for shading/lighting/texturing

http://vispy.org

Using Python for OpenGL is not a good idea. Knowhow of OpenGL is still required.

### Preprocessed 3D Graphics

http://3dmaps.ch/

OpenWebGlobe 2 - will be open sourced in Q2/Q3 2016


### Communities
- pybasel.ch
- Conference in June: geopython.net 2016 (in Basel)

## Audio
Matthieu Amiguet
https://twitter.com/MatthieuAmiguet
http://www.lescheminsdetraverse.net/
https://www.youtube.com/watch?v=fruvGfJ2Nis

### Basics
Library: PYO

### Reverb and Echo (Alphorn)
Freeverb = Reverb
Delay

### Canon
foocoo = foot button controller (pedals)

### Polyrythms

### Wah

## Coding / Decoding the Cosmos
Python Applications in Astrophysics

Chihway Chang

"Python is today everywhere in science."

Image of sizes

### Typical Python Libraries
- SciPy, NumPy, matplotlib, Sympy, pandas, seaborn, scikit-learn, astropy
- IPython, Jupyter

### Packages open-sourced by Astro Group
https://github.com/cosmo-ethz/hope
https://github.com/cosmo-ethz/CosmoHammer
https://github.com/cosmo-ethz/abcpmc

pynpoint.ethz.ch

### DES - Dark Energy Survey
http://www.spiegel.de/wissenschaft/weltall/dunkle-materie-dark-energy-survey-praesentiert-all-karte-a-1028503.html

### Drones for Calibration of Radio Telescopes

- 2 Telescopes at Bleien Observatory
- Drones from Koptershop
- Astrobites Blog http://astrobites.org/2015/06/02/drones/

## Scrapy
