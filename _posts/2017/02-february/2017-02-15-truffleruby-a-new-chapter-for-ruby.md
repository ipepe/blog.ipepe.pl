---
title: "TruffleRuby - A new chapter for Ruby?"
categories: programming
---

I recently found out about TruffleRuby project. Project describes itself as: 
```
A high performance implementation of the Ruby programming language. Built on the GraalVM by Oracle Labs.
```
It uses GraalVM:
```
GraalVM is a high-performance runtime that provides significant improvements in application performance and efficiency which is ideal for microservices.
```
And is based on Polyglot engine:
```
The Polyglot engine of the GraalVM allows the execution and interoperability of language interpreters for additional programming languages. This release of the GraalVM contains language interpreters for five well-known languages (JavaScript, Python, Ruby, R, and LLVM), and a teaching language (SimpleLanguage).
```

The basic idea is that You can mix many languages in one runtime. It is amazing idea, because if for example You found some javascript library that solves Your problem but You need it in Ruby, You can import that Javascirpt library and be on Your way.

It is also amazing, because initial benchmarks for TruffleRuby show performance improvement up to 9X over MRI Ruby

Sources:
 * <https://eregon.me/blog/2016/11/28/optcarrot.html>
 * <https://news.ycombinator.com/item?id=13398100> 


