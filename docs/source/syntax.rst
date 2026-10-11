Syntax
======

Rich can syntax highlight various programming languages with line numbers.

To syntax highlight code, construct a :class:`~rich.syntax.Syntax` object and print it to the console. Here's an example::

    from rich.console import Console
    from rich.syntax import Syntax

    console = Console()
    with open("syntax.py", "rt") as code_file:
        syntax = Syntax(code_file.read(), "python")
    console.print(syntax)

You may also use the :meth:`~rich.syntax.Syntax.from_path` alternative constructor which will load the code from disk and auto-detect the file type. The example above could be re-written as follows::


    from rich.console import Console
    from rich.syntax import Syntax

    console = Console()
    syntax = Syntax.from_path("syntax.py")
    console.print(syntax)


Line numbers
------------

If you set ``line_numbers=True``, Rich will render a column for line numbers::

    syntax = Syntax.from_path("syntax.py", line_numbers=True)


Theme
-----

The Syntax constructor (and :meth:`~rich.syntax.Syntax.from_path`) accept a ``theme`` attribute which should be the name of a `Pygments theme <https://pygments.org/demo/>`_. It may also be one of the special case theme names "ansi_dark" or "ansi_light" which will use the color theme configured by the terminal.


Background color
----------------

You can override the background color from the theme by supplying a ``background_color`` argument to the constructor. This should be a string in the same format a style definition accepts, e.g. "red", "#ff0000", "rgb(255,0,0)" etc. You may also set the special value "default" which will use the default background color set in the terminal.


Highlighting ranges
-------------------

Call :meth:`~rich.syntax.Syntax.stylize_range` to apply a style to a range of the code, for example to draw attention to a particular line. The range is given as a pair of ``(line_number, column)`` tuples, where line numbers start at 1 and columns start at 0::

    from rich.console import Console
    from rich.syntax import Syntax

    code = "def hello():\n    print('hello, world')\n"
    syntax = Syntax(code, "python")
    syntax.stylize_range("bold red", (2, 4), (2, 25))
    console = Console()
    console.print(syntax)

The style is applied on top of the syntax highlighting. Pass ``style_before=True`` to apply it underneath instead, so the theme's own styles take precedence where they overlap. Ranges that fall outside of the code are ignored.


Syntax CLI
----------

You can use this class from the command line. Here's how you would syntax highlight a file called "syntax.py"::

    python -m rich.syntax syntax.py

For the full list of arguments, run the following::

    python -m rich.syntax -h
    
