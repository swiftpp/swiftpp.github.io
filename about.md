---
layout: page
title: About
---

<img align="right" src="/images/logo-alpha-cropped-small.png">ll
The Swift++ Project is an effort to build a compiler which translates source code in
a Smalltalk-based language and generates binaries for the Swift and Objective-C environments, the goal being
to leverage the work of the Swift community to port the ecosystem to various platforms: desktop computers,
smartphones, servers, etc.

There are currently two repos the work is proceeding on:

* [Swift++](http://github.com/swiftpp/swiftpp) the official project repository for the Swift++ compiler
* [Swift](http://github.com/swiftpp/swift)     Apple's repo, where changes are tested until Swift++ build issues are resolved

Learn more and contribute on [GitHub](https://github.com/swiftpp).

## Setup

Building Swift requires 20 separate repositories to be cloned into a source tree hierarchy. To get to a compiler
which doesn't require those repos, and the 70GB of storage space a full, debuggable build requires, the Swift++
build system must be weaned off Swift's.

* Set up a development workspace for, and build, [Swift](http://github.com/apple/swift).
* Either clone the proving-ground branch into the Swift workspace, or the official repo into a separate
directory.
* Set an envirnoment variable **LLVM_BUILD_DIR** to point to the swift-llvm build directory.
(EG, export LLVM_BUILD_DIR="~/swift-source/build/Ninja-RelWithDebInfoAssert+swift-DebugAssert/llvm-macosx-x86_64")

Have questions or suggestions? Feel free to [open an issue on GitHub](https://github.com/swiftpp/swiftpp/issues) or [ask me on Twitter](https://twitter.com/swiftplusplis).

Thanks for reading!
