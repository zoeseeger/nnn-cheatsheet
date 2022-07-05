# Cheatsheet for nnn file manager

`alias nnn="nnn -deHr"`

### Commands

`space` : select\
`n` : new dir, file or symlink\
`p` : copy selected item to current dir\
`v` : move selected item to current dir\
`x` : delete\
`e` : editor\
`*` : make excecutable\
`d` : display type\
`r` : bulk rename in vi\
`.` : hidden files\
`?` : help\
`!` : console\
`1`, `2`, `3`, `4` : tabs\
`tab` : change tabs\
`cntrl+r` : rename current

### Profile variables

`EDITOR` :vim\
`NNN_BMS` : bookmarks list\
`NNN_PLUG` : plugins list\
`NNN_USE_EDITOR` : use editor number boolean\
`NNN_COLORS` : colours

### cd on exit - bash and zsh

```n ()
{
    # Block nesting of nnn in subshells
    if [ -n $NNNLVL ] && [ "${NNNLVL:-0}" -ge 1 ]; then
        echo "nnn is already running"
        return
    fi

    # The behaviour is set to cd on quit (nnn checks if NNN_TMPFILE is set)
    # If NNN_TMPFILE is set to a custom path, it must be exported for nnn to
    # see. To cd on quit only on ^G, remove the "export" and make sure not to
    # use a custom path, i.e. set NNN_TMPFILE *exactly* as follows:
    #     NNN_TMPFILE="${XDG_CONFIG_HOME:-$HOME/.config}/nnn/.lastd"
    export NNN_TMPFILE="${XDG_CONFIG_HOME:-$HOME/.config}/nnn/.lastd"

    # Unmask ^Q (, ^V etc.) (if required, see `stty -a`) to Quit nnn
    # stty start undef
    # stty stop undef
    # stty lwrap undef
    # stty lnext undef

    nnn -deHr "$@"

    if [ -f "$NNN_TMPFILE" ]; then
            . "$NNN_TMPFILE"
            rm -f "$NNN_TMPFILE" > /dev/null
    fi
}```
