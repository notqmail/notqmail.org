[[!templatebody <<ENDBODY
[<TMPL_IF DESC><TMPL_VAR NAME="desc"><TMPL_ELSE><TMPL_VAR NAME="name"></TMPL_IF>](https://github.com/notqmail/notqmail/compare/main...patches/notqmail/<TMPL_VAR ESCAPE=URL NAME="name">)
ENDBODY]]

## Description

To link to one of our rebased patch branches, use this template, specifying a value for the `name` parameter and optionally a `desc`.

## Examples

Link to [[!template id=patch name=ext-todo]]:

        \[[!template id=patch name=ext-todo]]
