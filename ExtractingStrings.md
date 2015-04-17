# Extracting strings #

`xgettext` doesn't have native support for Twig yet! Is for this why tags have the same syntax (use parentheses) as gettext functions for PHP or even C so xgettext could recognize and extract them.

Just add all your templates to the input files where xgettext has to extract string. For example, if you use that command to extract all string from .php files:

```
$ find include public_html -name '*.php' | xargs xgettext --language=C -o - > catalogue.pot
```

you should include the template directory and the file extension to include template files.

```
$ find include public_html templates -name '*.php' -o -name '*.html' | xargs xgettext --language=C -o - > catalogue.pot
```

Note that we are forcing use of C language to extract strings. If you use, for example, --language=PHP `xgettext` wouldn't extract any string since templates are not delimited by <?php and ?> tags.

`catalogue.pot` now will contain translatable strings from both PHP source code and template files.

Of course, you should use some other real settings while using xgettext, like --join-existing.