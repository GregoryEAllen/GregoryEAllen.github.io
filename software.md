---
layout: page
title: Software
permalink: /sw/
---

Given the nature of our business, ARL has a formal process that requires approvals before anything can be released to the public. Most of [my github projects](https://github.com/GregoryEAllen) were done on my own time, whether they were contributions to existing projects (e.g. [scipy](https://scipy.org) and [h5py](https://www.h5py.org)) or were my own new projects (e.g. [mlpolygen](https://github.com/GregoryEAllen/mlpolygen) and [fftw3cxx](https://github.com/GregoryEAllen/fftw3cxx)).

ARL has an independent research and development (IRAD) program that can be used to help fund publishable research and software in pursuit of graduate degrees (among other things). My larger public software releases were developed both on my own time and with the assistance of IRAD, and are subject to the same public release approvals.

### CPN

The [CPN software framework](https://github.com/GregoryEAllen/cpn) was partially funded by IRAD and was a component of my Ph.D. dissertation: "[Computational Process Networks: A Model and Framework for High-Throughput Signal Processing](https://users.ece.utexas.edu/~bevans/students/phd/greg_allen/)".

[My Process Networks page](../classic/ProcessNetworks/) provides some information and references about the formal models underlying CPN. The Process Network model also underlies [LabVIEW](https://en.wikipedia.org/wiki/LabVIEW) and [GNU Radio](https://www.gnuradio.org).
There were several releases to this framework spread over a number of years, and spanning [significant interruptions](../missing/) to my graduate studies. The oldest release was from [here](../classic/CPNSourceCode/) (2000), and later releases were from [here](../classic/CPN/) (2010-11) before moving to bitbucket and ultimately github.

The CPN framework is no longer used in this form, but many parts of the library have been extracted and used in other projects. For example, parts of the prime sieve case study made it into [mlpolygen](https://github.com/GregoryEAllen/mlpolygen), and [libvariant](https://github.com/GregoryEAllen/libvariant) was extracted and made into its own separate project.

### mlpolygen

[mlpolygen](https://github.com/GregoryEAllen/mlpolygen) is a tool that generates maximum length polynomials for [linear feedback shift registers](https://en.wikipedia.org/wiki/Linear-feedback_shift_register) (ML-LFSRs). These pseudo-random noise generators have great applications in communications ([m-sequence](https://en.wikipedia.org/wiki/Maximum_length_sequence)), cryptography, and hardware design verification. This scratched an itch for me, because I needed a bunch of maximum-length polynomials and was frustrated at how hard it was to evaluate them and find good ones.

It's amusing to me that this little tool has gotten a life of its own "on the outside". When my bitbucket projects went dark, a kind soul revived it from [archive.org](http://web.archive.org/web/20180820105651/https://bitbucket.org/gallen/mlpolygen) and now maintains his own fork at [github.com/hayguen/mlpolygen](https://github.com/hayguen/mlpolygen). It has also made it into the [Arch Linux user repository](https://aur.archlinux.org/packages/mlpolygen-git). I guess it scratches an itch for a few other people, too.

### LibVariant

[LibVariant](https://github.com/GregoryEAllen/libvariant) provides scripting-language-like variables (Variant) in C++, with serialization, schemas, and argument parsing. This tool was mostly conceived of and created by [John Bridgman](https://github.com/johnfb), my former graduate student and now colleague, while he was contributing to my [CPN framework](https://github.com/GregoryEAllen/cpn). It's included here because it was developed under my IRAD and was released alongside my other projects.

When we created LibVariant, we couldn't find any other standalone open source project that did the things we wanted for parsing and converting various standard text-based formats (e.g. XML, JSON, and YAML) that we were using to describe our Process Networks. LibVariant also provides [JSON Schema](https://json-schema.org) capabilities that we hadn't previously found elsewhere. If we were to start again today, we might build upon something like [nlohmann/json](https://github.com/nlohmann/json).

LibVariant is very heavily used throughout our laboratory for production software. As of Oct 2025 the current internal version is v1.9.0, but that has not been publicly released. We have not yet crossed the bridge to "maintain this project on the outside."

Some searching turns up signs that others have found LibVariant useful, such as the [microstacks/libvariant](https://github.com/microstacks/libvariant) and [ghostroute/libvariant](https://gitlab.com/ghostroute/libvariant) clones of our bitbucket repository, and some JSON Schema validation gists. There also exists a seemingly unrelated [end2endzone/libVariant](https://github.com/end2endzone/libVariant).

### MCSB

While I was nearing the end of writing my dissertation, I was also excitedly writing code for a follow-on idea: [MCSB, the Multi-Client Shared Buffer](https://github.com/GregoryEAllen/mcsb). MCSB is a high-throughput shared-memory publish-subscribe middleware suitable for implementing soft real-time systems on POSIX.

MCSB and its ecosystem has been wildly successful inside our laboratory, and is a foundational software component of the systems we build. Early versions of MCSB were written largely on my own time, and then later supported by IRAD.
MCSB was publicly released at v2.0.0, but the current internal version is v2.7.1 as of Sep 2025. Again, we have not yet crossed the bridge to "maintain this project on the outside."

[MCSB has its own page](../mcsb.html) with significantly more detail.
