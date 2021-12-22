---
title: "Bazel: Multi language Build Software for Monorepos"
date: 2021-12-04T18:49:08-05:00
tags: ["Bazel", "Build", "monorepo", "make"]
layout: post
---

Early on in my career I was responsible for compiling scientific software, installing them on HPC clusters to be used by scientists for their job runs. This is where I learned the 3 most used commands used when building and installing software. These ere `configure`, `make` and `make install`, as simple as that.

Fast forward years, code is longer just writing C or C++ code, these days most of the new software code is written in Golang, Python or Java just to name a few. For Golang there's `go build`, Python code be compiled into a binary but most commonly shipped as-is, and Java code can be build using Maven or Gradle building JAR files.

This means that developers are free to choose any languages, and more often than not, the software product might even be written in a few different languages. This creates a big challenge for Development and Build engineer in selecting a Build tool that can handle multiple languages, a tool that is robust and also scalable, while ensuring fast build times.

Enter [Bazel](https://bazel.build/).

Open source version of Google's internal build tool Blaze. Bazel provides a way to encapsulate entire software build process, provides fast build time using caching. It is written to provide reproducible build each time.

Bazel's principle is simple, If the inputs (source code) and parameters (running platform, build environment) haven't changed, the built output shouldn't change either. This means that each and every input has to be declared including outputs, based on these Bazel can ensure reproducibility (and correctness).

Bazel provides great benefits and can significantly cut down on built times of large monorepo projects. Among whole variety of features, Bazel also supports remote execution, which lets the developers perform their builds on a remote machines. This eliminates the need of large beefy laptops just so that developers are able to build code.

The tool also aims to provide a single way for both developer and Build system (such as Jenkins and others) use a common tool to perform builds.

Despite all its great feature, Bazel isn't widely adopted within industry which is largely due to do with Bazel's steep learning curve.
