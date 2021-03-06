---
title: Haskell in Leipzipg
subtitle: Detailed Program
---

Invited talk
------------

### Preserving Privacy with Monads ## {#russo}

*by [Alejandro Russo](http://www.cse.chalmers.se/~russo/)*

In a all-connected society, users consciously (or unconsciously) value their
privacy. Even skeptical people will recognize its importance; if they do not,
ask them to unlock their smartphone and hand it out to someone else---they will
most probably refuse!  Users want to have control on how their data gets
disseminated, specially today when private information gets handled by software
with heterogeneous trustworthiness---consider, for example, the various
smartphones apps with access to users' private photos, messages, and contacts
that exists today.  Unfortunately, current software practices are insufficient
to protect privacy: users who wish to benefit from software functionality are
often forced to grant access to their private data with no guarantees how it
gets handled. The key insight to guarantee privacy is not about granting or
denying access to private data, but ensuring that information only flows into
the appropriated places.

Information-Flow Control (IFC) is a research area dedicated to protect privacy
of data. Based on programming languages techniques, IFC scrutinizes source code
to track how data of different sensitivity levels (e.g., public or private)
flows within a program, where alarms are raised when privacy might be at stake.
IFC tools often provide specially designed compilers to build privacy-preserving
apps. Rather than building a compiler from scratch (a major task on its own),
Haskell plays a unique privileged role in this scenario: it can provide IFC
security via libraries. As long as developers program against the libraries'
API, code is secure by construction. This talk shows how to build such libraries
by specially designing monads capable to restrict the propagation of private
data. The presentation explores the different techniques used in a wide range of
libraries, namely LIO, MAC, and HLIO, where IFC is enforced dynamically (in the
form of an execution monitor), statically (by leveraging Haskell's type-system),
and as a combination of both.


**Short bio**: [Alejandro Russo] is an associate professor at Chalmers
University of Technology working on the intersection of functional languages,
security, and systems. He is the recipient of a Google Research Awards and
several grants from the Swedish research agencies Vetenskapsrådet, STINT, and
Barbro Osher foundation. Internationally, Prof. Russo worked on prestigious
research institutions like Stanford University, where he was appointed visiting
associate professor. His research ranges from foundational aspects of security
to developing tools to secure software written in Haskell, Python, and
JavaScript.

[Alejandro Russo](http://www.cse.chalmers.se/~russo/)

## Contributed Talks

### Automated Performance Measurements {#waldmann}

*by [Johannes Waldmann]*

### Generalized Algebraic Dynamic Programming: Theory and Applications in Bioinformatics and Linguistics {#stadler}
*by Sarah J. Berkemer, [Peter F. Stadler] and [Christian Hoener Zu Siederdissen]:*

### HGamer3D - a toolset for developing games with Haskell {#althainz}
*by Peter Althainz*

### Management at Algorithmic Financial Markets {#winschel}
*by Viktor Winschel*

### Project report: building a web-application with servant, lucid, and digestive-functors {#fischmann}
*by Matthias Fischmann and Andor Penzes:*

### Dependently Typed Heaps {#brunjes}
*by [Lars Brünjes]*


### Random access lists, nested data types and numeral systems {#komuves}
*by Balazs Komuves*

Random access lists, as introduced by Okasaki[^Oka95] [^Oka96], are persistent list-like
data structures with faster lookup than linked lists. This talk will be an explanation
of these data structures and their connection to numeral systems, with a small twist.
I claim no originality at all.

The core idea is that you can take a positional numeral system, like the usual binary,
ternary etc. numeral systems (or more esoteric ones, like the skew binary system), and
"categorify it", turning the length of a list (a number) into an actual sequence data type.
In place of the digits you will have tuples of (full) trees: For example in the decimal system,
if the digit at the hundreds place is 3, that will translate to a triple of 10-way trees,
each containing 100 elements at the leaves.

The usual linked list corresponds to the unary system; but with the non-unary systems, you
get O(log(k)) lookup, while modifying the left end of the list still remains on average O(1)
(worst case is typically O(log(n)), though guaranteed O(1) can be achieved too). They can be
also more compact in memory than linked lists (with GHC's in-memory representation).

Okasaki used the standard tree representation, which is one of the first data types one meets
when learning Haskell; for example, a leaf binary tree is represented as

```haskell
data Tree a
  = Leaf a
  | Node (Tree a) (Tree a)
```

However, full binary trees can be also represented by a nested data type:

```haskell
data Tree' a
  = Single a
  | Double (Tree' (a,a))
```

The word nested[^BM98] refers to the fact that the type parameter changes during the recursion.
Functions operating on such types require polymorphic recursion, an interesting language feature.
The nested binary tree has two advantages over the usual representation: First, the type system
guarantees that the tree is full (that is, every leaf has the same depth); second, since it lacks
the extra indirection at the leaves, it takes less memory (by two machine words per element, with GHC).
While the extra indirection can be also eliminated by modifying the original tree definition,
that would result in less elegant and more complicated code.

This idea can be applied to our list-like data structures, giving for example the following
very simple representation of leaf binary random-access lists:

```haskell
data Seq a
  = Nil                   -- the empty sequence
  | Zero   (Seq (a,a))    -- a sequence of even length
  | One  a (Seq (a,a))    -- a sequence of odd length
```

The implementation of the usual list operations is also very straightforward and simple
(a Haskell implementation can be found at[^KD16]). The same idea can be also applied to
the other variations. The resulting data structures are somewhat reminiscent of finger trees[^HP06],
which are also implemented using nested data types; however, these are much simpler (of course,
finger trees support more types of efficient operations).

A variation of the above idea uses the so-called skew numeral systems; these allow (modulo
implementation details) guaranteed O(1) cons, in exchange for a slightly more complicated
implementation. The resulting data structures use trees with data on both the nodes and the
leaves (which also results in more compact in-memory representation). Okasaki uses the skew
binary number system.


[^BM98]: Richard S. Bird and Lambert G. L. T. Meertens, Nested datatypes, Proceedings of the
         Mathematics of Program Construction, MPC '98, Springer-Verlag, 1998, pp. 52--67.

[^HP06]: Ralf Hinze and Ross Paterson, Finger trees: A simple general-purpose data structure,
        J. Funct. Program. 16 (2006), no. 2, 197--217.

[^KD16]: Balazs Komuves and Peter Divianszky, The nested-sequence Haskell library, 2016,
        http://hackage.haskell.org/package/nested-sequence.

[^Oka95]: Chris Okasaki, Purely functional random-access lists, In Functional Programming
        Languages and Computer Architecture, ACM Press, 1995, pp. 86--95.

[^Oka96]: Chris Okasaki, Purely functional data structures, Ph.D. thesis, Carnegie Mellon
        University, 1996.

### Plugin Architectures in Haskell {#graf}
*by Sebastian Graf*

### Store: An Efficient Binary Serialization Library {#kant}
*by Philipp Kant*

### Csound-expression Haskell framework for computer music {#kholomiov-talk}
*by Anton Kholomiov* (also see the corresponding [tutorial](#kholomiov-tutorial).)

The paper presents modern Haskell framework for creation of computer music.
It's called [csound-expression](http://github.com/spell-music/csound-expression/).  It's
EDSL for Csound audio programming language. The functional programming paradigm
can greatly enhance the process of text-based music production. We are going to
look at functional model for computer music.  It combines many aspects of
computer music. With the library we can create instruments from scratch apply
instruments to scores, trigger them with streams of events. We can create UIs
to control our music.

The key guiding principle of API design is modularity. Creation of
self-contained musical objects that can provide building blocks for the tower
of abstractions. The library is designed in such a way that every concept is
self contained and the whole program can be built from expressions. This
feature allows us to construct music in the interactive style. We can create
music in the REPL.

### Simple blog engine with shape functors and generic eliminators for ADTs {#penez}
*by Andor Penzes*

## Tutorials

### Efficient signal processing using Haskell and LLVM {#thielemann}
*by [Henning Thielemann]*

Haskell has so many features that are useful for signal processing:
Lazy evaluation allows for infinite lists,
simultaneous processing of a sequence of signal transformations and feedback,
monads allow for proper handling of coherent and incoherent sources of noise,
the type system allows for handling of sample rates via phantom types
and for hiding internal filter parameters in opaque types.
However, especially when relying on a lot of laziness
your Haskell programs will be pretty slow in any Haskell implementation.
In order to get reasonable processing speed
you need to switch from lazy lists of sampled displacements
to lazy lists of chunks of unboxed arrays.
This compromise is pretty close to how signals are usually stored
in signal processing packages written in machine oriented languages.
However, GHC still fails to generate efficient code
in cases that are hard to predict.
It may be due to missing inlining, too much sharing of functions
or too much laziness.

With the package `synthesizer-llvm`
we address the issue of efficient signal processing.
We use the LLVM Just-In-Time compiler
in order to perform signal processing with maximum speed.
LLVM provides optimization passes and vector instructions
that enable us to achieve this goal.
Our package also provides the programmer
precise control over strict evaluation,
code and data duplication or sharing.

In the tutorial we examine the examples included in the package,
experiment with them and learn about the basic concepts of the package this way.
The examples include:

 * Signal producers like oscillators and noise generator,
 * Frequency filters and how to work with internal filter parameters
   beyond the restricting scheme of audio and control rates
   found in other digital signal processing frameworks,
 * Sample value types: Stereo sounds, binary logic signals, fixed-size arrays
 * Causal signal processes with arrows,
   sharing and feedback with proven absence of deadlocks,
 * Express arrows by plain functions,
 * Composing sequences of sounds, composing music from tones,
 * MIDI control of sounds,
 * Integration with ALSA and JACK,
 * Vectorisation.

I already gave a tutorial on LLVM at [HaL-9](https://iba-cg.de/hal9.html)
and chose simple signal processing as application.
In this tutorial I will ignore the details of LLVM
and just concentrate on the signal processing part.
I do not plan to give an extensive introduction to signal processing,
the focus is on how to get things done with `synthesizer-llvm`.

Since LLVM changes slightly with every release
my LLVM bindings got a bit out of date.
I am currently updating them.
The tricky part to install is the package `llvm-ffi`.
If you want to attend the tutorial and want to code with us,
please send me your e-mail.
I will then notify you when my packages are ready for installation
and I will give you hints on the installation.


References:

 * [synthesizer-llvm](http://hackage.haskell.org/package/synthesizer-llvm)
   package at Hackage
 * Paper "Compiling Signal Processing Code embedded in Haskell via LLVM"
   at [arXiv](http://arxiv.org/abs/1004.4796)
 * [Demo of a song](https://www.youtube.com/watch?v=4zX0OnLGVV4)
   that is played live over a synthesizer-llvm based software synthesizer.


### Workshop: creating computer music with Haskell {#kholomiov-tutorial}
*by [Anton Kholomiov]* (also see the corresponding [talk](#kholomiov-talk).)

At the Workshop we are going to learn to create computer music with Haskell. 
We are going to produce buzzes and blips right in the REPL. Right in the ghci
you can create a midi-based instrument and complement it with drums and harmony
from your favorite library of samples or create the melody from scratch with scores
or event streams. Also we are going to learn how to create the UI-controllers on the 
fly with applicative style programming.

At the end of the workshop you should become en-armed with set of pro-quality synthesizers,
tools to create sample based music, trigger them the music in real time. We should discuss
some features unique to text-based programming. Have a glimpse at techniques used in musical generative art.

We are going to use the library
[csound-expression](http://github.com/spell-music/csound-expression/). It's a Haskell framework for sound design and music composition. It embeds very
powerful audio programming language Csound into Haskell. It's a Csound code generator.
The [Csound](http://csound.github.io/) is 30 years old audio programming language that embodies the wisdom of many researchers.
It has active community and it continues to evolve. It has the wide set of features (subtractive, granular,
waveguide, sample-based synthesis, physical modeling, spectral processing, emulators for many analog
synthesizer components)

The Haskell library complements the Csound with expressive language. We can use the great low-level
audio units of Csound and scheduler with higher level features of Haskell like higher order functions, rich
data type system, body of libraries for advanced data types.

Prerequisites:

To follow along you need to install several things:

* [csound-expression](http://hackage.haskell.org/package/csound-expression). It's a main library (available on hackage).
* [Csound compiler](http://csound.github.io/). The thing that converts code to audio (available on official site works on all platforms).
* other goodies based on core library: [csound-catalog](http://hackage.haskell.org/package/csound-catalog) and [csound-sampler](http://hackage.haskell.org/package/csound-sampler).
    They contain ready to use high quality patches (available on Hackage) and tiny DSL to compose music with audio-clips.
* the archive with audio files (drum loops and pads) that we are going to use. I'll publish it when closer to the date.

When everything installed check that it works. Open ghci import the module `Csound.Base` and type:

~~~
> dac (testDrone3 220)
~~~

Hit Ctrl+C to stop the playback. The library has minimal Haskell dependencies and should be easy to install. If something will go wrong with installation 
drop me a line on github or on the email that you can find on Hackage page of the project.

The library is really huge though the core is very simple and minimal. So I
recommend to read/skim through the [user guide of the
library](https://github.com/spell-music/csound-expression/blob/master/tutorial/Index.md).
That way you can get more out of the workshop.


### Ten example uses of monads {#schuster}
*by Philipp Schuster*


[Johannes Waldmann]: http://www.imn.htwk-leipzig.de/~waldmann/
[Peter F. Stadler]: http://www.bioinf.uni-leipzig.de/
[Christian Hoener Zu Siederdissen]: http://www.bioinf.uni-leipzig.de/~choener/index.html
[Lars Brünjes]:  https://github.com/brunjlar
[Anton Kholomiov]: https://github.com/anton-k
[Henning Thielemann]: http://dr.henning-thielemann.de/

