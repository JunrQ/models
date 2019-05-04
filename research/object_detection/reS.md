https://devguide.python.org/documenting/

http://docutils.sourceforge.net/docs/user/rst/quickref.html

## 7.3 reStructuredText Primer

* one asterisk for emphasis (italics)
* two asterisks for strong emphasis (boldface), and
* backquotes: ``text`` for code samples


* This is a bulleted list.
* It has two items, the second
  item uses two lines.

1. This is a numbered list.
2. It has two items too.

#. This is a numbered list.
#. It has two items too.


Literal code blocks are introduced by ending a paragraph with the special marker ::
The literal block must be indented:

This is a normal text paragraph. The next paragraph is a code sample::

   It is not processed in any way, except
   that the indentation is removed.

   It can span multiple lines.

This is a normal text paragraph again.


Use `Link text <http://target>`_ for inline web links. If the link text should be the web address, you don’t need special markup at all, the parser finds links and mail addresses in ordinary text.


Section headers are created by underlining (and optionally overlining) the section title with a punctuation character, at least as long as the text:

=================
This is a heading
=================

# with overline, for parts
* with overline, for chapters
=, for sections
-, for subsections
^, for subsubsections
", for paragraphs



An explicit markup block begins with a line starting with .. followed by whitespace and is terminated by the next paragraph at the same level of indentation. (There needs to be a blank line between explicit markup and normal paragraphs. This may all sound a bit complicated, but it is intuitive enough when you write it.)


A directive is a generic block of explicit markup. Besides roles, it is one of the extension mechanisms of reST, and Sphinx makes heavy use of it.

Basically, a directive consists of a name, arguments, options and content. (Keep this terminology in mind, it is used in the next chapter describing custom directives.) Looking at this example,

.. function:: foo(x)
              foo(y, z)
   :bar: no

   Return a line of text input from the user.




For footnotes, use [#]_ to mark the footnote location, and add the footnote body at the bottom of the document after a “Footnotes” rubric heading, like so:

Lorem ipsum [#]_ dolor sit amet ... [#]_

.. rubric:: Footnotes

.. [#] Text of the first footnote.
.. [#] Text of the second footnote.





7.4.5. Inline markup
As said before, Sphinx uses interpreted text roles to insert semantic markup in documents.

Names of local variables, such as function/method arguments, are an exception, they should be marked simply with *var*.

For all other roles, you have to write :rolename:`content`.

There are some additional facilities that make cross-referencing roles more versatile:

You may supply an explicit title and reference target, like in reST direct hyperlinks: :role:`title <target>` will refer to target, but the link text will be title.

If you prefix the content with !, no reference/hyperlink will be created.

For the Python object roles, if you prefix the content with ~, the link text will only be the last component of the target. For example, :meth:`~Queue.Queue.get` will refer to Queue.Queue.get but only display get as the link text.

In HTML output, the link’s title attribute (that is e.g. shown as a tool-tip on mouse-hover) will always be the full target name.

The following roles refer to objects in modules and are possibly hyperlinked if a matching identifier is found:

mod
The name of a module; a dotted name may be used. This should also be used for package names.

func
The name of a Python function; dotted names may be used. The role text should not include trailing parentheses to enhance readability. The parentheses are stripped when searching for identifiers.

data
The name of a module-level variable or constant.

const
The name of a “defined” constant. This may be a C-language #define or a Python variable that is not intended to be changed.

class
A class name; a dotted name may be used.

meth
The name of a method of an object. The role text should include the type name and the method name. A dotted name may be used.

attr
The name of a data attribute of an object.

exc
The name of an exception. A dotted name may be used.

The name enclosed in this markup can include a module name and/or a class name. For example, :func:`filter` could refer to a function named filter in the current module, or the built-in function of that name. In contrast, :func:`foo.filter` clearly refers to the filter function in the foo module.

Normally, names in these roles are searched first without any further qualification, then with the current module name prepended, then with the current module and class name (if any) prepended. If you prefix the name with a dot, this order is reversed. For example, in the documentation of the codecs module, :func:`open` always refers to the built-in function, while :func:`.open` refers to codecs.open().




