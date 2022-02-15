# Cheatsheet for nnn file manager

### Commands

`n` : new dir, file or symlink\
`p` : copy selected item to current dir\
`v` : move selected item to current dir\
`x` : delete\
`*` : make excecutable\
`d` : display type\
`?` : help\
`space` : select\
`1`, `2`, `3`, `4` : tabs

### Profile variables

`NNN_BMS` : bookmarks\
`NNN_PLUG` : plugins\
`NNN_USE_EDITOR` : use editor\
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
