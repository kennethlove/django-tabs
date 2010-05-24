Provides a set of template tags for managing tabs in Django templates. You set your tabs in a block in the parent template,defining markup for active or non-active tabs. In child templates you then decide which tabs are active.

Usage: once you have installed the app in your PYTHONPATH, add "tabs" to your INSTALLED_APPS as with any other app.

In your parent template (for example, base.html):

.. code-block::
    {% load tabs %}
    {% block navigation %}
    <ul id="top-nav">
        <li><a href="/" class="{% ifactivetab "topnav" "home" %}active{% else %}inactive{% endifactivetab %}">Home</a></li>
        <li><a href="/cart" class="{% ifactivetab "topnav" "cart" %}active{% else %}inactive{% endifactivetab %}">My cart</a></li>
    ....
    </ul>
    {% endblock %}

Then in your child template (for example, index.html):

.. code-block::
    {% extends "base.html" %}
    {% load tabs %}
    {% block navigation %}
    {% activetab "topnav" "home" %}
    {{ block.super }}
    {% endblock %}

This will create this HTML:

.. code-block::
    <ul id="top-nav">
        <li><a href="/" class="active">Home</a></li>
        <li><a href="/cart" class="inactive">My cart</a></li>
    ...
    </ul>

The template tags are:

.. code-block::
    ifactivetab (namespace) tab ( else ) endifactivetab

Sets the conditions for what markup is displayed if the tab is active or not. The namespace argument is optional, you don't need it if you only have one set of tabs in a page. This lets you maintain several sets of tabs - for example a main navigation menu and a secondary section-specific menu.

.. code-block::
    activetab (namespace) tab

Sets the active tab. Set this in the same block you defined your tabs, and then call block.super so the tabs are rendered.

