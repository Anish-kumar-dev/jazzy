![jazzy](logo.jpg)

![analytics](https://ga-beacon.appspot.com/UA-50247013-2/jazzy/README?pixel)

![Test Status](https://travis-ci.org/realm/jazzy.svg?branch=master)

jazzy is a command-line utility that generates documentation for your Swift or
Objective-C projects.

Both Swift & Objective-C projects are supported.

*Objective-C support was recently added, so please report any issues you find.*

Instead of parsing your source files, jazzy hooks into [Clang][clang] and
[SourceKit][sourcekit] to use the [AST][ast] representation of your code and
its comments for more accurate results.

jazzy’s output matches the look & feel of Apple’s official reference
documentation, post WWDC 2014.

![Screenshot](screenshot.jpg)

### Requirements

* A version of [Xcode][xcode] (6.x or 7.x) capable of building the Swift project
  you wish to document, installed in a location indexed by Spotlight.

### Installing

To install jazzy, run `[sudo] gem install jazzy` from your command line.

### Usage

Run `jazzy` from your command line. Run `jazzy -h` for a list of additional
options.

You can set options for your project’s documentation in a configuration file,
`.jazzy.yaml` by default. For a detailed explanation and an exhaustive list of
all available options, run `jazzy --help config`.

#### Swift

Swift documentation is generated by default.

As an example, this is how Realm Swift docs are generated:

```shell
jazzy \
  --clean \
  --author Realm \
  --author_url https://realm.io \
  --github_url https://github.com/realm/realm-cocoa \
  --github-file-prefix https://github.com/realm/realm-cocoa/tree/v0.96.2 \
  --module-version 0.96.2 \
  --xcodebuild-arguments -scheme,RealmSwift \
  --module RealmSwift \
  --root-url https://realm.io/docs/swift/0.96.2/api/ \
  --output docs/swift_output \
  --template-directory docs/templates
```

#### Objective-C

To generate documentation for Objective-C headers, you should pass `--objc`,
`--umbrella-header ...` and `-framework-root ...` as parameters to jazzy.

As an example, this is how Realm Objective-C docs are generated:

```shell
jazzy \
  --objc \
  --clean \
  --author Realm \
  --author_url https://realm.io \
  --github_url https://github.com/realm/realm-cocoa \
  --github-file-prefix https://github.com/realm/realm-cocoa/tree/v0.96.2 \
  --module-version 0.96.2 \
  --umbrella-header Realm/Realm.h \
  --framework-root . \
  --module Realm \
  --root-url https://realm.io/docs/objc/0.96.2/api/ \
  --output docs/objc_output \
  --template-directory docs/templates
```

or AFNetworking:

```shell
jazzy \
  --objc \
  --author AFNetworking \
  --author_url http://afnetworking.com \
  --github_url https://github.com/AFNetworking/AFNetworking \
  --github-file-prefix https://github.com/AFNetworking/AFNetworking/tree/2.6.2 \
  --module-version 2.6.2 \
  --umbrella-header AFNetworking/AFNetworking.h \
  --framework-root . \
  --module AFNetworking
```

### Troubleshooting

#### Swift: Only extensions are listed in the documentation.

By default, jazzy only documents public declarations. To generate documentation
for declarations with a lower accessibility level (internal or private), please
set the `--min-acl` flag to `internal` or `private`.

### Development

jazzy is composed of two parts: the parser ([SourceKitten][SourceKitten],
written in Swift) and the site generator (written in ruby).

To build and run jazzy from source, you'll first need [bundler][bundler]. Once
bundler is installed, run `bundle install` from the root of this repo. At this
point, run jazzy from source by running `bin/jazzy`.

Instructions to build SourceKitten from source can be found at
[SourceKitten's GitHub repository][SourceKitten].

### Design Goals

jazzy's main design goals are:

- Generate source code docs matching Apple's official reference documentation
- Support for standard Objective-C and Swift documentation comment syntax
- Leverage modern HTML templating ([Mustache][mustache])
- Leverage the power and accuracy of the [Clang AST][ast] and [SourceKit][sourcekit]
- Support for Dash docsets
- Support Swift & Objective-C (*mixed projects are a work in progress*)

### License

This project is under the MIT license.

[clang]: http://clang.llvm.org "Clang"
[sourcekit]: http://www.jpsim.com/uncovering-sourcekit "Uncovering SourceKit"
[ast]: http://clang.llvm.org/docs/IntroductionToTheClangAST.html "Introduction To The Clang AST"
[xcode]: https://developer.apple.com/xcode "Xcode"
[SourceKitten]: https://github.com/jpsim/SourceKitten "SourceKitten"
[bundler]: http://rubygems.org/gems/bundler
[mustache]: http://mustache.github.io "Mustache"
