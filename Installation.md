# Installation and configuration #

Just add these lines when registring the Twig Autoloader function:

```
<?php
    require_once "/path/to/lib/Twig/Autoloader.php";
    Twig_Autoloader::register();
    require_once "/path/to/gettexttwig.php";
    GettextTwig::register();

    ...

    $loader = new Twig_Loader_Filesystem("path/to/templates");
    $twig = new Twig_Enviroment($loader, $twig_options_array);
    $twig->addExtension(new GettextTwig());
?>
```