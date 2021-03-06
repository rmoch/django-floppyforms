Provided widgets
================

.. _widgets:

Default widgets for form fields
-------------------------------

The first column represents the name of a django.forms field. FloppyForms aims
to implement all the Django fields with the same class name, in the
``floppyforms`` namespace.

======================== =================== ========================
Fields                   Widgets             Specificities
======================== =================== ========================
BooleanField             CheckboxInput
CharField                TextInput
ComboField               TextInput
ChoiceField              Select
TypedChoiceField         Select
FilePathField            Select
ModelChoiceField         Select
DateField                DateInput           <input type="date">
DateTimeField            DateTimeInput       <input type="datetime">
DecimalField             NumberInput         <input type="number">
EmailField               EmailInput          <input type="email">
FileField                ClearableFileInput
FloatField               NumberInput         <input type="number">
ImageField               ClearableFileInput
IntegerField             NumberInput         <input type="number">
MultipleChoiceField      SelectMultiple
TypedMultipleChoiceField SelectMultiple
ModelMultipleChoiceField SelectMultiple
NullBooleanField         NullBooleanSelect
TimeField                TimeInput           <input type="time">
URLField                 URLInput            <input type="url">
SlugField                SlugInput           <input pattern="[-\\w]+">
RegexField               TextInput           <input [pattern=...]>
IPAddressField           IPAddressInput      <input pattern=...>
MultiValueField          None (*abstract*)
SplitDateTimeField       SplitDateTimeWidget
======================== =================== ========================

.. note:: ClearableFileInput

    The ``ClearableFileInput`` widget has been added in Django 1.3. If you use
    django-floppyforms with Django 1.2, the ClearableFileInput will behave
    just like a traditional FileInput.

    .. versionchanged:: 1.0
       django-floppyforms 1.0 ships with a full backport of
       ``ClearableFileInput``.


.. note:: TypedMultipleChoiceField

    The ``TypedMultipleChoiceField`` has also been added in Django 1.3, it
    will behave like a normal ``MultipleChoiceField`` on Django 1.2.


.. note:: RegexField

    In Django, ``RegexField`` takes a required ``regex`` argument. The version
    shipped in floppyforms also takes an optional ``js_regex`` argument, for
    client-side validation of the regex. The ``js_regex`` must be a regex
    written in javascript syntax. Example::

        class RegexForm(forms.Form):
            re_field = forms.RegexField(r'^\d{3}-[a-z]+$',  # regex
                                        '\d{3}-[a-z]+')     # js_regex

    If you don't provide the ``js_regex`` argument, there will be no
    client-side validation of the field. Although the the two versions of the
    regex may be identical, the distinction allows you to pass compiled
    regexes as a ``regex`` argument.


Extra widget
------------

Django provides "extra" widgets in ``django.forms.extras.widgets``. In fact, a
single extra widget is implemented: ``SelectDateWidget``. The template-based
version is available under the ``floppyforms.SelectDateWidget`` name.

By defaut, this widget with split the date into three select (year, month and
day). You can overload the template so that it is displayed in a different
order or with 3 inputs:

.. code-block:: jinja

       <input type="text" name="{{ day_field }}" value="{{ day_val|stringformat:"02d" }}" id="{{ day_id }}"{% for attr in attrs.items %} {{ attr.0 }}="{{ attr.1 }}"{% endfor %} />
       <input type="text" name="{{ month_field }}" value="{{ month_val|stringformat:"02d" }}" id="{{ month_id }}"{% for attr in attrs.items %} {{ attr.0 }}="{{ attr.1 }}"{% endfor %}/>
       <input type="text" name="{{ year_field }}" value="{{ year_val|stringformat:"04d" }}" id="{{ year_id }}"{% for attr in attrs.items %} {{ attr.0 }}="{{ attr.1 }}"{% endfor %}/>

Other (HTML5) widgets
---------------------

Some HTML5 widgets are also provided, although browser support may not be
there yet:

* ``SearchInput``: a widget that renders ``<input type="search">``.
* ``ColorInput``: ``<input type="color">`` (not implemented in any browser
  yet).
* ``RangeInput``: ``<input type="range">``, for sliders instead of spinboxes
  for numbers.
* ``PhoneNumberInput``: ``<input type="tel">``. For phone numbers.
