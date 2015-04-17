# Usage in templates #

Gettext-Twig provides a set of tags corresponding to each PHP gettext available function.

## gettext ##
`gettext` tag looks for a message in the current domain.

```
{% gettext (<message>) [<parameter> {, <parameter> }] %}
```

Next sample will print "Hello World!" in the current locale.

```
{% gettext ("Hello World!") %}
```

The short alias for ´gettext´ is also allowed:

```
{% _("Hello World!") %}
```

All Gettext-Twig tags allows printf-style parameters. For example:

```
{% gettext ("Welcome back, %s!") user.name %}
```
Would print in spanish "Hola otra vez, Ana" when `user.name` is "Ana".

Some modifications must be done when `gettext` is used within HTML attributes due these are externally quoted and xgettext will ignore internal quoted strings:

```
<input type="submit" name="save_preferences" value="{% _("Save preferences") %}" />
```

`xgettext` wont extract _Save preferences_ due (as parsing as C code) the string would be "{% _)", since the first quote have precedence over the second.
To solve this you can escape the quote with Twig:_

```
<input type="submit" name="preferences" value={{ '"' }}{% _("Save preferences") %}" />
```

## ngettext ##
`ngettext` tag is the plural form of `gettext`.

```
{% ngettext (<message_singular>, <message_plural>, <count>) [<parameter> {, <parameter> }] %}
```

Next sample will print "There are 5 users" in the current locale and in the correct locale plural form, when users.count is 5.

```
{% ngettext ("There is one user", "There are %d users", users.count) users.count %}
```

## dgettext ##
`dgettext` tag does the same as ´gettext´ but overriding the current domain.

```
{% dgettext (<domain>, <message>) [<parameter> {, <parameter> }] %}
```

## dngettext ##
`dngettext` tag is the plural form of `dgettext`.

```
{% dngettext (<domain>, <message>, <count>) [<parameter> {, <parameter> }] %}
```

## dcgettext ##
`dcgettext` tag does the same as ´dgettext´ but overriding the category.

```
{% dcgettext (<domain>, <message>, <category>) [<parameter> {, <parameter> }] %}
```

_category_ is one of the following values:

  * LC\_ALL for all of the below
  * LC\_COLLATE for string comparison, see [strcoll()](http://www.php.net/manual/en/function.strcoll.php)
  * LC\_CTYPE for character classification and conversion, for example [strtoupper()](http://www.php.net/manual/en/function.strtoupper.php)
  * LC\_MONETARY for [localeconv()](http://www.php.net/manual/en/function.localeconv.php)
  * LC\_NUMERIC for decimal separator (See also [localeconv()](http://www.php.net/manual/en/function.localeconv.php))
  * LC\_TIME for date and time formatting with [strftime()](http://www.php.net/manual/en/function.strftime.php)
  * LC\_MESSAGES for system responses (available if PHP was compiled with libintl)


## dcngettext ##
`dcngettext` tag is the plural form of `dcgettext`.

```
{% dngettext (<domain>, <message_singular>, <message_plural>, <count>, <category>) [<parameter> {, <parameter> }] %}
```