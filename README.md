### xwinmo v0.2.0.0 [GNU GPLv3]

`xwinmo`(1) is a simple bash shell script, that wraps up some `wmctrl`(1) actions to provide processing of more than one X window. Therefore, `xwinmo`(1) is used in combination with `xwinpp`(1).

#### Install

* Get the newest version of `xwinmo`(1) with `$ git clone https://github.com/D630/xwinmo.git` or
  download its last release on https://github.com/D630/xwinmo/tags
* Make `xwinmo` executable and copy it elsewhere into `<PATH>`

Explicitly required:
`GNU bash`(1), `wmctrl`(1), `xprop`(1), [xwinpp](https://github.com/D630/xwinpp) >= v0.1.2.6

#### Options

```
-I, --input-file= <FILE> or hyphen (-)
      Obtain output of xwinpp(1) from <FILE>. If hyphen, get output by
      reading from standard input.

-1, --workarea-x= <PX>
      Specify the left edge of the workarea.

-2, --workarea-y= <PX>
      Specify the top edge of the workarea.

-3, --workarea-w= <PX>
      Specify the <WIDTH> of the workarea.

-4, --workarea-height= <PX>
      Specify the <HEIGHT> of the workarea.

-A, --action= <HACT>
      Specify action of action --hide.

-D, --desk= <DESK>
      Move windows to desktop <DESK>.

-e, --entity= <ENT>
      Specify the entity of actions --move and --size.

-R, --reference= <REF>
      Used with action --move and --size. If entity is 'pro', specify
      the reference.

-g, --geo= <GEO>
      Specify the geometry of actions --move and --size.

-d, --direction= <DIREC>
      Used with action --move and '-R window' as reference.

-V, --active
      Tell xwinmo(1) to perform --move and --size on active window and then
      to aboort.

-W, --switch
      Used with action -M to switch to the desktop after moving.
```

#### Subcommands

```
-h, --help
      Display a short help.

-v, --version
      Print current version of xwinmo(1).

-c, --close
      Close windows gracefully.

-H, --hide
      Add, remove or toggle window property 'hidden', specified with
      option -A.

-f, --focus
      Switch to the desktop containing the windows, raise the
      windows, and give them focus. At the end, focus the active
      window again.

-M, --move-to-desk
      Tell xwinmo(1) to move windows to another desktop. Specify
      this action with options -D and -W.

-s, --size
      Tell xwinmo(1) to size windows. The sizing is specified by
      options -e, -R, -g and -V.

-m, --move
      Tell xwinmo(1) to move windows. The moving is specified by
      options -e, -R, -g, -d and -V.
```

#### Arguments

```
<FILE>                  File may be a regular file or a named pipe.
<PX>                    Pixel size specified by an integer.
<DESK>                  'curr' or relative to the current desktop
                        'next' or 'prev'. Specify a desktop
                        number (starts at 0) with the prefix 'i:'; a
                        desktop name is prefixed with 's:'.
                        Examples: 'i:0'; 's:web'; ''s:some stuff''.
<ENT>                   Can be 'px' or 'pro', what means 'pixel'
                        and 'procent'.
<HACT>                 'add', 'remove' or 'toggle'.
<REF>                   Can be 'window', 'win' or 'workarea', 'wa'.
<DIREC>                 Can be 'north', 'east', 'south', 'west' or
                        'n', 'e', 's', 'w'.
<GEO>
            <X>         Pixel x size specified by an integer.
            <Y>         Pixel y size specified by an integer.
            <W>         Pixel width size specified by an integer.
            <H>         Pixel height size specified by an integer.
            <PRO>       Procent size specified by an integer.
            _           Means, that old size is kept.

            Samples:
                        '<X>,<Y>', '<W>,<H>', '<PRO>,<PRO>', '<PRO>'
            Examples:
                        size -e pro -R win -g '<PRO>,<PRO>'
                        size -e px -g '<W>,<H>'
                        move -e pro -R win -d east -g '<PRO>'
```

#### Examples

To move windows:

```
xwinpp -I ./list -p | xwinmo -I - -m -V -e px -g 640,800
xwinpp -I ./list -p | xwinmo -I - -m -e pro -R workarea -g 50,_
xwinpp -I ./list -p | xwinmo -I - -m -e pro -R window -g 100 -d east
xwinpp -I ./list -p | xwinmo -I - -M -W -D i:1
xwinpp -I ./list -D i:1 -p | xwinmo -I - -M -D curr
```

#### Environment

`XWINMO_INPUT_FILE`
Use this instead of option `-I`.

#### Notes

- You may write all commands and options without masking `--`. So,
instead of `--help` you may use `help`.
- If no workarea geo is set, `xwinmo`(1) uses `<_NET_WORKAREA>`.

#### To do

See file [TODO](../master/doc/TODO.md)

#### Bugs & Requests

Report it on https://github.com/D630/xwinmon/issues
