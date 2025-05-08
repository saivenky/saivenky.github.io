---
layout: post
title: "x86 Python on M1 Macbooks"
categories: dev
created: 2023-02-17
redirect_from: /2023/02/17/x86-python-on-m1-macbooks
---
This is a very niche post. But if you happen to need an `pyenv`-managed, x86-version of Python installed on your Apple M1 Macbook, then you can follow these steps. It's super simple once you know what approach to take. Figuring out the simplest approach was the hard part.

### Prerequisites

Based on the title and first sentence of this article, I'm going to assume you already have Homebrew and `pyenv` installed using standard steps for an M1 Macbook (i.e. you didn't do anything special for x86).

Taking some inspiration from [this post](https://towardsdatascience.com/how-to-use-manage-multiple-python-versions-on-an-apple-silicon-m1-mac-d69ee6ed0250), you'll need to install an x86-version of Homebrew and create an alias for `brew86`.

Install Homebrew and setup `brew86`:

```shell
# Standard Homebrew installation command but with the arch prefix
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Add this to your .bashrc or .zshrc
alias brew86='arch -x86_64 /usr/local/bin/brew'
```

*Tip*: `arch`
Each Homebrew installation tells you slightly different directions for activating it within your environment.

For M1, this typically looks like adding the following to your `.zshrc`:

```
eval "$(/opt/homebrew/bin/brew shellenv)"
```

For x86 (Intel) version on Mac, this is:

```
eval "$(/usr/local/bin/brew shellenv)"
```

*If you don't immediately see the difference, it's in the start of the path to Homebrew. And if you're asking why: These are [decisions made by Homebrew](https://docs.brew.sh/Installation).*

You will need to swap between these two (so make sure the place where you added that line in your `.zshrc` is easily accessible).

When I say M1- or x86- version of Homebrew "active", I mean include that specific version of the `eval` line in your `.zshrc`.

### Installation of `x86` Version of Python

With the x86-version Homebrew active in your shell (restart shell after you make the change to your `.zshrc`), run the following:

1. Install `pyenv`:

```
brew install pyenv
```

2. Install Python with `pyenv`. For example:

```
PYENV_VERSION_SUFFIX="_x86" arch -x86_64 pyenv install 3.8.15
```

Now switch back to M1 Homebrew (and restart your terminal). And that's it!

### Why does this work?

`pyenv` is just a shim in your terminal. It's just a shell function. It's not an executible. So when you change architectures (i.e. swapping between M1 or x86 Homebrew) and install `pyenv` in each, you're not doing much except letting you run `pyenv` easily in either.

The `eval "$(...brew shellenv)"` line is where all the magic happens. Homebrew sets the correct `PATH`, etc. This is also why when you setup `pyenv` once, there is no need to add it again to your `.zshrc`. The `eval` line just makes sure you use the `pyenv` that's in your path.

When you install `pyenv` via Homebrew, it also installs the necessary additional packages needed like `openssl` or `readline`, which are needed to build Python. Luckily `pyenv` looks at the currently active Homebrew when it tries to link all the libraries for the Python build steps. So the x86 Homebrew installs the x86 `openssl`, which gets linked with the x86 Python.

When you switch back to M1 Homebrew, as mentioned before, `pyenv` is just a shell function. All the plugins and Pythons installed in one "version" are available to the other.
