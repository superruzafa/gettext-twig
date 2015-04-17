[Twig](http://www.twig-project.org) is a modern, scalable and fast template system for [PHP](http://php.net). However before 0.9.5 it lacks full [gettext](http://www.gnu.org/software/gettext/) support.

Since version 0.9.6 Twig implements gettext support through `{% trans %}` tag, being able to translate single strings (gettext) and strings that might have a plural form (ngettext). However one must to search and write manually all of these strings since xgettext is unable to extract them.

This extension allows you to take advantage of all the power of gettext to translate templates and its related commands (as xgettext) to extract all strings from them.