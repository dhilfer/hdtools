hdtools: some sort of useful command line tools

- [INSTALLATION](#installation)
- [DESCRIPTION](#description)

# INSTALLATION

hdtools are pure sh-scripts (not even bash is required), so they shall
run on any \*nix like target around.

To install a particulart tool right away type:

```sh
    export GET_THIS_TOOL=<some_tool>; sudo curl -L https://raw.githubusercontent.com/dhilfer/hdtools/${GET_THIS_TOOL}-latest/${GET_THIS_TOOL} -o /usr/local/bin/${GET_THIS_TOOL}; sudo chmod a+rx /usr/local/bin/${GET_THIS_TOOL}; unset GET_THIS_TOOL
```

To install them all type:
(or replace 'curl -L <url> -o <target>' with 'wget <url> -O <target>' if curl is not available on your system)

```sh
    export GET_THIS_TOOL=hdgrep; sudo curl -L https://raw.githubusercontent.com/dhilfer/hdtools/${GET_THIS_TOOL}-latest/${GET_THIS_TOOL} -o /usr/local/bin/${GET_THIS_TOOL}; sudo chmod a+rx /usr/local/bin/${GET_THIS_TOOL}; unset GET_THIS_TOOL
    export GET_THIS_TOOL=hdfind; sudo curl -L https://raw.githubusercontent.com/dhilfer/hdtools/${GET_THIS_TOOL}-latest/${GET_THIS_TOOL} -o /usr/local/bin/${GET_THIS_TOOL}; sudo chmod a+rx /usr/local/bin/${GET_THIS_TOOL}; unset GET_THIS_TOOL
    export GET_THIS_TOOL=hdontarget; sudo curl -L https://raw.githubusercontent.com/dhilfer/hdtools/${GET_THIS_TOOL}-latest/${GET_THIS_TOOL} -o /usr/local/bin/${GET_THIS_TOOL}; sudo chmod a+rx /usr/local/bin/${GET_THIS_TOOL}; unset GET_THIS_TOOL
```

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

Nearly every tool will have a **--verbose** option to show the real
executed commands and related annotations.

Some tools have a **--dry** option, which will just show the real
commands without execution. This one is useful to add some more
~~unsupported~~ user-specific options or just to copy-/paste commands to
another machine, or custom scripts.

## Short overview of available tools and features

Basic motivation for **hdgrep** and **hdfind** can be understand here at [XKCD](https://xkcd.com/1168/)

Both tools will store last search results in a file, named
**hdgrep.$(whoami).last_result**. By default either in '*/tmp/*' or (on X11 env)
'*/run/user/<user_id>/*'. This can be used to quick sync your search
results with your favourite editor.

### hdgrep
This tool performs (primary) a text search within files. For that it
uses *grep* and *find*.

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
This is basically a wrapper to find command, increasing its usability.

![hdfind_example](https://github.com/dhilfer/hdtools/blob/main/doc_assets/hdfind_example.gif?raw=true)

> Example usage of hdfind



