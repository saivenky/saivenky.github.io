---
layout: post
title: "Makefiles Make Life Hard"
categories: dev
created: 2023-01-27
date: 2023-01-27
redirect_from: /2023/01/27/makefiles-make-life-hard
---
As a software engineer, part of your role is to reduce complexity. The more you need to juggle in your head, the worse the solution. Being a "clever" coder that likes to show off your mental acrobatics is bad for long term maintainability.

Personally, my memory is really bad. If there's a reason *not* to remember something, I will choose not to remember it. (I literally don't even remember my age sometimes. I remember my birthday and then work forwards from there.)

Makefiles are bad because they force me to remember things.

Makefiles exist in the realm of running commands and dependencies in a shell. They should look consistent within the environment they exist. For the most part, this looks true, but it's the small nuances that drive me crazy.

### Assumptions

Let's start with assumptions and my perception of the world:
* Bash and Zsh are the most popular shell terminals. Bash is the default in Linux and Zsh is now the default for Macs. When you install Cygwin or use WSL within Windows, the default shell is Bash. I don't use or know much about the popularity of Powershell, but my next assumption shows why I'm not really exploring it further.
* Makefiles are primarily used to manage compiled languages needing ordered "steps" in order to compile your code. What I'm talking about is languages like C, C++, or Java. All these languages have intermediate steps before producing a final executable product.

I'm going to make a final assumption that people that work with compiled languages are not afraid to work in a terminal (I'm a bit skeptical of Java developers, but let's stick with that assumption).

People that work in other languages are likely to use other build and dependency systems. This is also why I'm excluding Java developers because it's much more likely to prefer something like Gradle or Maven doing Java development.

I'm just trying to hammer the point that there is a strong correlation between Makefile users and using Bash/Zsh.

So why is this a problem?

### Shell Syntax

In shell, you define a variable like so:

```shell
export EXPORTED_VARIABLE="i'm available everywhere"
# or
VARIABLE="i'm available only within the script"
```

You can use a variable like this:

```shell
echo $VARIABLE
# or be safe and do
echo "$VARIABLE"
# or be explicit and do
echo "${VARIABLE}"
```

Notice in that last line that we're using curly braces (i.e. `{` and `}`).

When you need to run arbitrary commands and do something with the output, you can do this like so:

```shell
LINES=`cat my_file.txt | sort | uniq | wc -l`
# or
ANOTHER_WAY="$(cat another_file) | sort | uniq | wc -l)"
```

Notice in the last line that we're using parentheses (i.e. `(` and `)`).

Another thing to note is that you **cannot** put spaces between the variable name and value.

### Makefile Syntax

If you've worked with Makefiles before, you already know the point I'm about to make.

In Makefiles, you define a variable like so:

```make
VARIABLE := "some value"

my_target:
    echo this is $VARIABLE

ifdef $VARIABLE
another_target:
    echo variable was set
endif
```

What do you get when you run:
```shell
make my_target
make another_target
```

You get 💩:
```
❯ make my_target
echo this is ARIABLE
this is ARIABLE
❯ make another_target
make: *** No rule to make target `another_target'.  Stop.
```

The counter-intuitive output is precisely the reason I dislike Makefiles. Let's look at an equivalent shell script.

### Intuitive Results in Shell Scripts

```shell
# filename: my_script.sh

VARIABLE="some value"

function my_target() {
    echo this is $VARIABLE
}

if [ -n $VARIABLE ]
    function another_target() {
        echo variable was set
    }
fi
```

What do you expect if you run:
```shell
source my_script.sh
my_target
another_target
```

It's exactly what I expect 💙:
```
❯ my_target
this is some value
❯ another_target
variable was set
```

### Fixing Makefile Syntax

Now let's pretend like you knew shell syntax you suspect the variable reference is at fault, so you try an alternative. Instead of just writing `$VARIABLE`, you write `${VARIABLE}`.

```make
my_target:
    echo this is ${VARIABLE}

ifdef ${VARIABLE}
another_target:
    echo variable was set
endif
```

That doesn't work either. You get a syntax error at the conditional statement. Okay, let's look up how to do it and fix it...

```make
ifdef VARIABLE
```

What?! This is absolutely not what I expect. But alright, we got it working.

Now what if I want to execute a command? Let's change `my_target`:

```make
my_target:
    echo this Makefile has $(cat Makefile | wc -l) lines
```

💩 again:

```
❯ make my_target
echo this Makefile has  lines
this Makefile has lines
```

The issue is that `$(...)` is not a valid way to run a command and get it's output. Only backticks are valid. In fact, the more surprising thing is that `$(...)` is also a valid way to reference a variable.

```make
my_target:
    echo this Makefile has `cat Makefile | wc -l` lines
    echo variable is set to $(VARIABLE)
```

Output:
```
❯ make my_target
echo this Makefile has `cat Makefile | wc -l` lines
this Makefile has 10 lines
echo variable is set to "some value"
variable is set to some value
```

### Takeaway

Don't use Makefiles. Makefiles are a trap. They're appealing because it looks similar to writing shell scripts, but as we've seen, they're not similar. They're more appealing because they're already installed by default on Linux machines. This is also a convenience trap.

If you must resort to it, put only the minimal amount of logic in there. Push everything else out into something else more serious.

Use build systems more specific to your language. For C or C++, consider using Bazel. For Java, you have Gradle or Ant. Some languages have their own build systems (e.g. Rust) and others need package management instead of a build system (e.g. using Poetry for Python).
