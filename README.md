# hdtools: some sort of useful command line tools

- [INSTALLATION](#installation)
- [DESCRIPTION](#description)
    - [hdgrep](#hdgrep)
    - [hdfind](#hdfind)
    - [hdontarget](#hdontarget)
    - [hdpack](#hdpack)
    - [hdunpack](#hdunpack)


# INSTALLATION

hdtools are pure standalone sh-scripts (bash is not required), so they
shall run on any \*nix like target around.

Basically copy desired tool somewhere on your target and start to use
it.

You can do a simple install for \<tool> (e.g.: hdgrep) like this:

```sh
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdgrep; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
```

Due to github's URL policy you'll need a tool which is able to handle
*https://* URL's. This is may not available on some of your tiniest
initramfs-busybox. Beware of this constraint, or just put the tools
somewhere on your local network and host by yourself (ajust
**UPGRADE_LATEST_RELEASE_LINKS** var within the code, or control it
trough ENV).

I wget does not support https:// on your system, try to replace:
```sh
wget <url> -O <target>
```
with
```sh
curl -L <url> -o <target>
```

If wget/curl struggle with github's https:// certifikate (e.g. due
time/date etc. on your embedded sys) you can use
(wget)--no-check-certificate or (curl)--insecure flag.


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
special to get them running. You'll mostly need the: *coreutils* and
*sed*. For hdgrep/hdfind you'll additionally need *grep*, *find* and
*xargs*. For hdontarget *openssh* or *dropbear*. For hdpack/hdunpack
*tar*, *gzip*, *xz*, etc.

This shall be available on any \*nix platform, as well as on
Cygwin/git-like environments on Windows.

Please read the related **--help/-h** of particular tool to learn more
about its special dependencies and needs.

Use the **--verbose** option to show the real executed commands and
related annotations.

Use **--dry** option, which will just show the real commands without
execution. This one is useful to add some more ~~unsupported~~
user-specific options or just to copy-/paste commands to another
machine, or custom scripts.


## Short overview for available tools and features

Basic motivation for **hdgrep** and **hdfind** can be understand
here at [XKCD](https://xkcd.com/1168/)

Both tools will store last search results in a file, named
**hdgrep.$(whoami).last_result**. By default either in '*/tmp/*' or
(on X11 env)'*/run/user/<user_id>/*'. This can be used to quick sync
your search results with your favourite editor.


### hdgrep
This tool performs (primary) a text search within files. For that it
uses **grep** and **find**.

Type to install:

```sh
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdgrep; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
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
sudo apt install ripgrep
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
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdfind; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
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
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdontarget; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
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

### hdpack

This tool is a wrapper for **tar -cf** providing possibility to quick
pack stuff.

By default hdpack will pack a ".tar.gz" file, which can be changed to
".tar.xz" or ".zip".

If packing a ".zip" an optional password can be specified.

Type to install:

```sh
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdpack; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
```

Type to update:

```sh
hdpack --upgrade
```


### hdunpack

This tool is a wrapper for a bunch of other tools, such as **tar**,
**ar**, **xz**, **bz2**, **unzip**, **7z**, etc. trying to quick
un-pack given files.


Type to install:

```sh
# may you'll need to be root, or just set P=${HOME}/bin or whatever

export T=hdunpack; export P=/usr/local/bin; wget https://raw.githubusercontent.com/dhilfer/hdtools/main/${T} -O ${P}/${T}; chmod a+rx ${P}/${T}; unset T; unset P
```

Type to update:

```sh
hdunpack --upgrade
```

Run hdunpack with --help, to see currently supported formats:
```sh
hdunpack -h
(2.1.1)hdunpack: (try to) unpack stuff
Usage: hdunpack [OPTIONS] [--] unpack_this [unpack_this ...]

hdunpack currently supports following compressions(file formats),
respectively related tools
  .tar  :   tar (without compression)
  .7z   :   7zip
  .zip  :   unzip
  .rar  :   unrar
  .ar   :   ar
  .cpio :   cpio

following compressions can additionally be part of a .tar archive
  .gz   :   gzip, pigz(multicore)
  .xz   :   xz, pixz(multicore)
  .bz2  :   bzip2
  .zst  :   zstd
  .lz4  :   lz4
  .lzma :   lzma
  .lzo  :   lzop
  .lz   :   lzip
```
