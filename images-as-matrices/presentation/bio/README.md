(the conference site requested a biography; I decided to sketch a very brief one.)

### main theme

My main research focus has been to find, study, and develop a **high-level computer programming formalism
allowing to deform programs in a continuous fashion** (just as one can deform recurrent neural networks in a continuous fashion).

I was trying to approach this problem from various angles: doing research in the mathematics of continuous domains
for denotational semantics of programming languages, studying theoretical neuroscience, and so on.

Finally, our research collaboration was starting to see the hints of the possible solution from approximately Fall of 2012,
and the formalism for continuously deformable programs was developed by our research collaborations in 2015-2016. 

These days I am continuing to focus on studying and experimenting with this formalism and I am hoping that it will
eventually stop being a purely research subject and will become a technology.

I maintain a Web site for this formalism here: https://anhinga.github.io/

I also maintain a list of open problems and promising research and technological directions and interdisciplinary
connections related to this formalism: https://www.cs.brandeis.edu/~bukatin/dmm-collaborative-research-agenda.pdf

### brief timeline

My background in software, mathematics, and science goes back to Soviet Union, to machine code, Algol-60, Fortran-4,
and to punched cards; to Pushchino, the Biological Center of the Soviet Academy of Sciences, and to
the Mathematical class of Moscow High School number 7.

I started to focus on continuous models of computations in college, then emigrated to USA, worked as
a scientific programmer for Alex Rashin at Biosym Technologies doing computational geometry and computational chemistry
(I was the second author on several papers in _The Journal of Physical Chemistry_ and _Biophysical Chemistry_
from that period), then did a PhD in Computer Science at Brandeis University focusing of mathematics
of continuous domains for denotational semantics (this is a copy of my 2002 PhD thesis: https://arxiv.org/abs/1512.03868).

In parallel, I worked in various places in the software industry. There I had a chance to first touch
dataflow programming, Lisp, and actor model of programming. 

This century I have been working at a geographic software company (ownership of it went through acquisitions, spin-offs,
and such, so one very long employment looks like several shorter ones from a formal viewpoint), 
while doing research in parallel. My research focus was mostly on theoretical neuroscience for a while,
then a research collaboration on deep connections between _partial metrics_ and _fuzzy equalities_, 
and finally (from approximately Fall of 2012) a research collaboration
on deep connections between _partial contradictions_ and _vector semantics of programming languages_ 
and, from 2014-2015 on, a series of research collaborations on _neuromophic computations with linear streams_. 

Starting from about 2011 I was gradually moving from just being a lover of computer animation and electronic music to
my first attempts to make some visual, audio, and audio-visual art of my own, and I am continuing to make new computer art every few months or so.
It involved playing a bit with MilkDrop 2 for WinAmp, mixing music a bit with Serato DJ,
doing a lot of animations and a bit of sound work in Processing, doing a tiny bit of that in Clojure,
and finally working a bit with shader-based GLSL animations.

### 2015-present

_Linear streams_ are streams for which linear combinations of several streams are defined. If one makes sure that
linear computations and general (often non-linear) computations are interleaved, then one gets continuously deformable programs which
we call **Dataflow matrix machines (DMMs)**. Another way to obtain DMMs is to start with recurrent neural networks
and replace streams of numbers with linear streams and allow complicated "activation functions"
(that is, transformations of linear streams) with arbitrary arity.

This setup also allows these neural machines to have very natural and flexible self-modification facilities.
There are toy implementations in Processing with mutable matrices, and reference implementation in Clojure with
immutable streams of tree-shaped "flexible-rank tensors". The reference paper on DMMs is https://arxiv.org/abs/1712.07447

I hope to create the next application of this formalism in Julia 
(both **Julia Flux** and **JAX** are the machine learning frameworks which finally have sufficient flexibility
we need to take full advantage of the flexibility of DMMs). I started to switch to Julia in the early 2020.
I recently sketched a three-page note outlining my hopes in this sense: https://www.cs.brandeis.edu/~bukatin/towards-practical-dmms.pdf
