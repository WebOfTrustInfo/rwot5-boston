# Overview

## Essentials

-   Smart-signatures (smart contracts) supporting metalanguage.
-   Minimal scheme-ish; loosely based on [r5rs](http://www.schemers.org/Documents/Standards/R5RS/), with some changes:
    -   NO call/cc (undelimited continuations) as those break capabilities
    -   But delimited continuations are great, if we can get those in,
        awesome
    -   Will we support hygenic macros?
    -   Type annotations (required or optional)?  There are a couple
        of options to explore:
        -   [Hackett](http://docs.racket-lang.org/hackett/guide.html)
    -   [SRFI-71](https://srfi.schemers.org/srfi-71/srfi-71.html) let/let\*/letrec.  r5rs already specifies multiple value
        return (a great feature!) but utilizing them via call-by-values
        is painful.
-   Uses restricted base environment + lexical scope to implement
    [Jonathan Rees' security kernel based on lambda calculus](http://mumble.net/~jar/pubs/secureos/secureos.html)
    (See also [Andy Wingo's blogpost on the subject](https://wingolog.org/archives/2011/03/19/bart-and-lisa-hacker-edition))
-   Must also be constrained in both space and time
    -   space: Execution is done within a limited memory environment
    -   time: Implementations may need to "count" execution steps and
        halt a program that runs for too many steps.
-   execution environment
    -   compiles to native code for production, with appropriate obfuscation
        to prevent side channel attacks
    -   however "development environment" can be more loose for fast
        "live hacking" (have a mutable toplevel, do type checking only at
        runtime)
    -   Many lisps have long supported both interpreted and compiled
        code so we don't need to "make a choice"
-   ISO-8859-1 strings only (sorry! unicode strings would require
    adding a whole lot of tooling to the language)
-   Can be normalized to [canonical s-expressions](http://people.csail.mit.edu/rivest/Sexp.txt).  The "display hints"
    feature could be used for type annotations (there's some chance we'll
    have to extend it to not just support a single atom but even full
    s-expressionsfor compound objects of types which aren't just the
    language primitives)
-   Some particular core types and procedures will need to be supplied
    for smart signatures support (linked data slice & dice, signature
    verification, and???)

## Up for consideration

-   Do we want to support any record types?
    (Property lists can always be used, though it may be desirable to
    have a better type structure for the sake of a type system)
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
    of legal signatures.  An equitable estoppel defense may work, though
    it would be better to encode into the blockchain somehow that some
    licensing choice has been made.  Perhaps Wikipedia is a good example
    of the largest collaborative commons; using a copyleft license that
    is used by all parties by default could result in "solidifying" the
    structure into a legally enforceable/protected commons.  (Other
    routes for blockchains that would prefer more permissive/lax
    licenses may include encoding the expected de-facto license into
    the genesis block.)

# Implementation milestones

-   Spec out language concepts (type annotation is the biggest decision;
    r5rs already has the rest)
-   Write a toy metacircular evaluator prototype of what the language
    "looks like" (this should be fast for an experienced schemer
    (task to Chris Webber or some other schemer?))
-   Real implementation has a number of different paths, but suggested:
    Implement on Guile's compiler tower with bottom layer first targeting
    VM then targeting native code generation.
