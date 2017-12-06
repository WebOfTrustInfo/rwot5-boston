# Smarm: Requirements for a smart-signatures Scheme

By Christopher Lemmer Webber and Christopher Allen

## Overview

[Smart signatures](https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/draft-documents/smarter-signatures.md)
are desirable, but how to implement them?
We need a language that is powerful and flexible enough to meet our
needs while safe and bounded to run while remaining simple enough
to feasibly implement.

[Scheme](https://en.wikipedia.org/wiki/Scheme_programming_language)
is a turing-complete language with a (at least stated) fondness for
minimalism.
Unfortunately Scheme on its own is neither "safe" nor (necessarily)
deterministic.
Thankfully we can get the properties we want through:

-   Making object capabilities a core part of the language.
    Specifically, [Jonathan Rees' "W7 security kernel"](http://mumble.net/~jar/pubs/secureos/secureos.html)
    demonstrates that a pure lexically scoped environment *is itself*
    an appropritate substrate for object capabilities.
-   Restricting space and time precisely in a way that is
    deterministic and reproducible.
-   Removing sources of external side effects.

Thus the name "Smarm" is indeed quite smarmy, as Smarm is not a new
language, but a configuration of existing language ideas, most of them
relatively (for the world of computer programming) old, repurposed for
new problem domains.
(We will need to specify exactly what the primitives of the language
are, as well as their associated costs... and perhaps that's where
"Smarm" is a good name for this dialect of a dialect of Lisp.)

What follows is a listing of requirements and notes to make this
language possible.

## Essentials

-   Smart-signatures (smart contracts) supporting metalanguage
    means evaluation of a program as predicate.
    Any "state" should be passed in as arguments to the program.
-   Loosely based on [r5rs](http://www.schemers.org/Documents/Standards/R5RS/), with some changes:
    -   NO call/cc (undelimited continuations) as those break capabilities
    -   But delimited continuations are great, if we can get those in,
        awesome.  Some analysis on how delimited continuations affect
        capabilities, and the extent to which they are useful
        (or overkill) in the described system should be explored.
    -   Will we support writing hygenic macros within the language?
        Some constructs supplied to the base environment will be
        written within hygenic macros, but whether a user of the
        language can feasibly use syntax-rules / syntax-case and
        friends is up for debate.
        Passing macros between modules in something like W7 which
        fundamentally (?) is a run-time system may turn out to be
        difficult.
    -   [SRFI-71](https://srfi.schemers.org/srfi-71/srfi-71.html) let/let\*/letrec.  r5rs already specifies multiple value
        return (a great feature!) but utilizing them via call-by-values
        is painful.
-   Uses restricted base environment + lexical scope to implement
    [Jonathan Rees' security kernel based on lambda calculus](http://mumble.net/~jar/pubs/secureos/secureos.html)
    (See also [Andy Wingo's blogpost on the subject](https://wingolog.org/archives/2011/03/19/bart-and-lisa-hacker-edition))
-   Must also be constrained in both space and time
    -   space: Execution is done within a limited memory environment
        (can this be done consistently without having to assign our own
        costs / implementing our own garbage collector?)
    -   time: Implementations may need to "count" execution steps and
        halt a program that runs for too many steps.
-   execution environment
    -   compiles to native code for production, with appropriate obfuscation
        to prevent side channel attacks
    -   however "development environment" can be more loose for fast
        "live hacking" (have a mutable toplevel, etc)
    -   Many lisps have long supported both interpreted and compiled
        code so we don't need to "make a choice"
-   ISO-8859-1 strings only (sorry! unicode strings would require
    adding a whole lot of tooling to the language).
    (Possibly we could call these "bytestrings" and leave open
    the possibility of unicode strings for later?
    Beware the lessons of Python 2 -> Python 3!)
-   Source code can be normalized to
    [canonical s-expressions](http://people.csail.mit.edu/rivest/Sexp.txt).
    The "display hints" feature could be used for type annotations,
    though this could also be done by tagging list structures
    (both are supported in [guile-csexps](https://gitlab.com/dustyweb/guile-csexps)
    for instance).
-   Some particular core types and procedures will need to be supplied
    for smart signatures support (linked data slice & dice, signature
    verification, and???).
    These could be part of the "base language", though this opens up
    a debate of just how large the base system should be and where
    modules (or even simply supplying utilities as arguments to the
    program) fit in.

## Up for consideration

-   Type annotations?
    These are not necessarily "necessary", as our language is already
    appropriately constrained.
    Adding type annotations may even complexify implementation
    significantly.
    Nonetheless, there are a couple of options to explore:
    -   [Hackett](http://docs.racket-lang.org/hackett/guide.html)
    -   [Typed Racket](https://docs.racket-lang.org/ts-guide/)
-   Do we want to support any record types?
    (Property lists can always be used, though it may be desirable to
    have a better type structure for the sake of a type system.)
    However, it is possible to construct new types that even fit
    nicely into the object capability model using a combination of
    vectors and `seals` from
    [W7](http://mumble.net/~jar/pubs/secureos/secureos.html).
-   It may be desirable to use [Guile's compiler tower](https://www.gnu.org/software/guile/manual/html_node/Compiler-Tower.html) for the initial
    implementation.  While production code MUST NOT run in the Guile
    virtual machine, Guile's compiler tower supports switching out
    different layers, including different outputs (for example, you can
    run Javascript OR scheme at the top and export to the virtual machine
    bytecode OR [even Javascript at the bottom](https://lists.gnu.org/archive/html/guile-user/2017-08/msg00070.html) (WIP)).  This could allow
    for a "fast to iterate" development environment for users using
    something like Emacs + Geiser (or whatever your equivalent editor is)
    while exporting to native code or even something like WebAssembly.
    However, the output of the native code verison MUST be able to run
    *without* Guile's language environment.
-   It would be possible to add a module system that can actually import
    other nodes from the blockchain to execute them.  This would then
    allow the blockchain itself to become a library of code.
-   In the United States and mostly-internationally, "All Rights
    Reserved" is the default copyright.  We're now talking about adding
    what's recognized as a fully usable language to a blockchain, which
    means that if someone were to push code to the blockchain that
    others evaluated and claimed "Oh, you're running my code, now you
    need a license" this is possibly a valid legal form of attack against
    blockchain participants who are automatically verifying the integrity
    of smart signatures.  An equitable estoppel defense may work, though
    it would be better to encode into the blockchain somehow that some
    licensing choice has been made.  Perhaps Wikipedia is a good example
    of the largest collaborative commons; using a copyleft license that
    is used by all parties by default could result in "solidifying" the
    structure into a legally enforceable/protected commons.  (Other
    routes for blockchains that would prefer more permissive/lax
    licenses may include encoding the expected de-facto license into
    the genesis block.)

## Implementation milestones

-   A toy implementation has been written making use of
    [Guile's sandboxed evaluation](https://www.gnu.org/software/guile/manual/html_node/Sandboxed-Evaluation.html)
    facilities (public git repository coming soon after some cleanup).
    This works, but:
    -   Restrictions on space and time are not deterministic.
    -   We would still want native compilation with obfuscation to
        prevent side-channel attacks.
-   Real implementation has a number of different paths, but suggested:
    Implement on Guile's compiler tower with bottom layer first targeting
    VM then targeting native code generation.
