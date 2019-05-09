<img align="right" src="/images/logo-alpha-cropped-small.png">

## Welcome to the Swift++ Project Page

  Swift++ is a fork of Swift to develop a compiler that matches the performance envelope
  of Swift, but having the readability and elegance of Smalltalk. By basing this compiler
  on the Swift ecosystem, we'll take advantage of the popularity of the system as it's
  ported to platforms as diverse as desktop machines, smartphones and servers. Now that
  Swift 5 has been released and has standardized the Swift ABI stability & its process
  for future enhancements, we can build on that groundwork to ensure Swift++ code will
  remain compatible with Apple's future plans for the language and its ecosystem.

## Swift++ Objectives

  - Implement a programming language to replace Objective-C, which Apple is deserting.
    Unlike Swift, the Swift++ language will actually be like Objective-C, but without the C (so
	it looks like Smalltalk).

	- The base syntax for Swift++ is Smalltalk, so code for other Smalltalk implementations would,
	depending on frameworks and libraries used, be compatible.

	- Extend the Smalltalk syntax to support strong typing and other facilities offered by Objective-C
	and Swift as warranted.

	- Starting with a fork of the current Swift compiler, modify the lexical analyzer and parser to
	match the syntax objectives listed above.

	- To further support code portability from Pharo and other Smalltalk derivatives, a separate
	  tool or environment would support fileIns.

  - Implement (or port) regular Smalltalk classes as expected.

  - Implement a compiler with bare-bones functionality, focusing on compilation speed, interoperability, and
    portability.
	
	- Remove syntax, functionality, and features which come from Swift and are not essential to
	expressing the programmer's intent.

  - Implement a programming system which will be compatible with the Swift ecosystem Apple favors.

    - The compiler should be usable in the Swift environment, via command line, Xcode, or whatever.

	- The linker in Swift's environment should have no difficulty linking Swift++ object files into
	  a Swift module, a library, archive, framework or executable.

	- Compiled Swift++ code should support interoperability with Swift, Objective-C, C, and C++. That's
	  a tall order, I know, but LLVM/Clang are used to build the binaries, so most of the work's already
	  done.

## Current Status

  I'm currently using a tree hierarchy separate from the Swift tree hierarchy to isolate the components.
  I use environment variable **LLVM_BUILD_DIR** to point to the LLVM build directory ('llvm-{host}-{arch}).
  I've modified the build script `utils/build-script` to generate the build system and build the project.
  It builds to `swiftpp-{PLATFORM}` in an out-of-tree build, but running the front-end (`swiftpp`)
  directly fails (for me in this configuration) with the error

  ```
<unknown>:0: error: unable to load standard library for target 'x86_64-apple-macosx10.14'
  ```

  Running `swiftpp` within the debugger in the same build tree works, though.

  The compiler (`swiftppc`) can parse code, but I haven't gotten it to generate an executable, nor to link
  objects into an Objective-C or Swift executable. But, then again, I've never written or built a
  Swift app before either. I guess it's about time to learn. ;)

  More details to follow, but now it's time to build stuff!
