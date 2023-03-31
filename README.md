# hdtools: some sort of useful command line tools

- [INSTALLATION](#installation)
- [DESCRIPTION](#description)
    - [hdgrep](#hdgrep)
    - [hdfind](#hdfind)
    - [hdontarget](#hdontarget)


# INSTALLATION

hdtools are pure sh-scripts (bash is not required), so they shall
run on any \*nix like target around.

For example to install hdgrep type:

```sh
sudo wget https://raw.githubusercontent.com/dhilfer/hdtools/main/hdgrep -O /usr/local/bin/hdgrep
sudo chmod a+rx /usr/local/bin/hdgrep
```

Due to github's URL policy you'll need a tool which is able to handle
*https://* URL's. This is may not available on some of your tiniest
initramfs-busybox. Beware of this constraint, or just get the tools
somewhere on your local network and host by yourself (ajust
**UPGRADE_LATEST_RELEASE_LINKS** within the code, or control it trough
ENV var).

Try to replace *'wget \<url> -O \<target>'* with *'curl -L \<url> -o \<target>'*
if wget does not support https:// on your system.


# DESCRIPTION

## Foreword

This is a small collection of tools that I use for my daily dev work on
embedded linux systems.

The tools are written in pure sh-script and shall be compatible to any
sh flavor out there.
Tested so far on  **bash**, **dash**, **ash**, **busybox sh** and
(git-)**sh.exe**.

Being mostly just a *wrapper* utilizing 'real' cmd-tools, *hdtools*
shall be seen as helper to increase usability and productivity for your
daily business.


## Dependencies and Requirements

Since all tools are written in shell you don't really need anything
special to get them running. You'll mostly need the: *coreutils*, *sed*,
*grep*, *xargs* and *find*. This shall be available on any \*nix
platform, as well as on Cygwin/git-like environments on Windows.

Please read the related **--help/-h** of particular tool to learn more
about its special dependencies and needs.

Use the **--verbose** option to show the real executed commands and related 
annotations.

Use **--dry** option, which will just show the real commands without 
execution. This one is useful to add some more ~~unsupported~~ user-specific 
options or just to copy-/paste commands to another machine, or custom scripts.


## Short overview for available tools and features

Basic motivation for **hdgrep** and **hdfind** can be understand here at [XKCD](https://xkcd.com/1168/)

Both tools will store last search results in a file, named
**hdgrep.$(whoami).last_result**. By default either in '*/tmp/*' or (on X11 env)
'*/run/user/<user_id>/*'. This can be used to quick sync your search
results with your favourite editor.


### hdgrep
This tool performs (primary) a text search within files. For that it
uses **grep** and **find**.

Type to install:

```sh
sudo wget https://raw.githubusercontent.com/dhilfer/hdtools/main/hdgrep -O /usr/local/bin/hdgrep
sudo chmod a+rx /usr/local/bin/hdgrep
```

Type to update:

```sh
hdgrep --upgrade
```

Thank to [Rust](https://www.rust-lang.org/) there is a "insanely fast"
searching tool named *[ripgrep](https://github.com/BurntSushi/ripgrep/releases)*
which does exactly the same with better performance.

hdgrep will use ripgrep(*rg*) by default if it's available.
Since ripgrep is shipped with all major distros all you'll need to do is
something like:

```sh
sudo apt-get install ripgrep
```

![hdgrep_example](https://github.com/dhilfer/hdtools/blob/main/doc_assets/hdgrep_example.gif?raw=true)

> Example usage of hdgrep

hdgrep offers more useful searches utilising some other tools than grep.
For example you can search in pdf-files using *pdfgrep*, or in object
files using *nm*.

![hdgrep_pdf_example](https://github.com/dhilfer/hdtools/blob/main/doc_assets/hdgrep_pdf_example.gif?raw=true)

> Searching in pdf files using pdfgrep

![hdgrep_obj_bin_example](https://github.com/dhilfer/hdtools/blob/main/doc_assets/hdgrep_obj_bin_example.gif?raw=true)

> Searching in object files using nm (-o) and bingrep (-b)


### hdfind

This is basically a wrapper to **find** command, increasing its usability.

Type to install:

```sh
sudo wget https://raw.githubusercontent.com/dhilfer/hdtools/main/hdfind -O /usr/local/bin/hdfind;
sudo chmod a+rx /usr/local/bin/hdfind;
```

Type to update:

```sh
hdfind --upgrade
```

![hdfind_example](https://github.com/dhilfer/hdtools/blob/main/doc_assets/hdfind_example.gif?raw=true)

> Example usage of hdfind


### hdontarget

This tool is wrapper for **ssh/scp/dropbear** which can be used to
automate scripts (and workflows) if working with remote network targets.

Type to install:

```sh
sudo wget https://raw.githubusercontent.com/dhilfer/hdtools/main/hdontarget -O /usr/local/bin/hdontarget
sudo chmod a+rx /usr/local/bin/hdontarget
```

Read the detailed help to see, what hdontarget can do for you:

```sh
hdontarget --help
```

Type to update:

```sh
hdontarget --upgrade
```

Look at available usage examples

```sh
hdontarget --help-examples
```
