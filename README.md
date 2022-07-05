# Cheatsheet for nnn file manager

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

    export NNN_TMPFILE="${XDG_CONFIG_HOME:-$HOME/.config}/nnn/.lastd"

    nnn "$@"

    if [ -f "$NNN_TMPFILE" ]; then
            . "$NNN_TMPFILE"
            rm -f "$NNN_TMPFILE" > /dev/null
    fi
}
