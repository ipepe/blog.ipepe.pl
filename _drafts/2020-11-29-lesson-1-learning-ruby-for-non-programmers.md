---
title: Learning Ruby for non-programmers - Lesson 1 - Basic types, operators and conditions
categories: tutorials
---

## Preparations

* install rbenv
    * homebrew required?
* rbenv install 2.6.4 (or other relevant ruby version)
* setup github
    * setup ssh identity
* download rubymine

## Terminal

Terminal is a way of running programs without GUI (Graphic User Interface). Most of programmer tools are command line programs. Some of basic terminal programs are:
	* ls - list files and directories in current working directory
	* pwd - show current working directory
	* cd - change directory (example: cd `/Users/Patryk/Downloads`)
	* cat - print file contents to terminal window

## Ruby

### Files and executing programs
Ruby programming language that is classified as high level. It means that it was built with simplicity of use in mind, and it doesn’t require managing Your program’s memory.

To create a ruby program file, You create a file that has words delimetered with dashes or underscores and file extesion is `.rb`

To run (execute) a ruby program You can run `ruby your-program-file-name.rb`

## Lesson 1 - Basic types, operators and conditions

### Basic Types

Programming is purely about processing data. In Ruby we have 4 basic data types that can be processed:
	* nothing, null (nil)
	* numbers (1, 2.5, 10_000)
	* booleans (true/false)
	* strings (“text”)

### IRB - 

IRB - Short for Interactive Ruby, is a quick way to explore the Ruby programming language and try out code without creating a file. IRB is a Read-Eval-Print Loop, or REPL, a tool offered by many modern programming languages. To use it, you launch the irb executable and type your Ruby code at the prompt. IRB evaluates the code you type and displays the results.

### Basic operators

You can use Ruby like You would use a calculator. Start `irb` in terminal and type:
`5+3`

Ruby interpreter should respond with:
`=> 8`

Seems pretty anticlimactic for all of that work to just be able to calculate two numbers.

But You can also try doing same with text:

`”we finish each other’s “ + “sandwiches”`

And irb should respond with: 
`=> ”we finish each other’s sandwiches”`

You can also try:
`“10” + “10”`

And Ruby’s IRB should respond:
`=> “1010”`

At first look, You probably thought: `Wait! It’s broken! This is stupid! My calculator is smarter than this!`. 

But this is intended behaviour, Ruby did exactly what You asked. And You asked to combine two text’s that contained characters 1 and 0. You didn’t specify that they should be treated, and because data type was String, it joined two texts together. This is first example of program doing something other than what You were thinking about doing. Get used to it :)

You should also try:
`“10” - “10”`

And Ruby’s IRB should respond:
```
NoMethodError (undefined method `-' for "10":String)
Did you mean?  -@
```

There is no operator `-` for Strings, and Ruby informed You about this saying `undefined method ‘-‘ for “10”:String`. While `+` is pretty clear that You want to join two texts, unfortunately `-` isn’t defined, because by intuition it’s hard to understand what would You want to achieve.

### Hello world

Up to this point, our code didn’t do much useful. Let’s jump into “Hello world” convention.

It’s an unwritten (or maybe it’s written somewhere) rule that when You try a new programming language, You write a program that outputs “Hello world”.

In ruby this is quite simple:
```ruby
puts “Hello world!”
```

`puts` is global method, to read more You can take a look into Ruby documentation here: https://ruby-doc.org/core-2.7.2/Kernel.html#method-i-puts

When You execute this code, it should print in terminal: `Hello world!`

This is amazing! Your first program doing something!

Let’s change it, so that program greets You! I will put my name, but You should put Yours.

```ruby
puts “Hello Patryk!”
```

Now this is something useful. A machine greeting human by name! Well, usefulness is limited to humans named `Patryk` how about we change that.

First, we need to extract name into variable. (what? variable?)

```ruby
name = “Patryk”
puts “Hello “ + name + “!”
```

Variables are used to store information to be referenced and manipulated in a computer program. They also provide a way of labeling data with a descriptive name, so our programs can be understood more clearly by the reader and ourselves. It is helpful to think of variables as containers that hold information. Their sole purpose is to label and store data in memory. This data can then be used throughout your program.








