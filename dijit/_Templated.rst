#format dojo_rst

dijit._Templated
================

:Authors: Peter Higgins, Bill Keese, Nikolai Onken
:Project owner: Bill Keese
:Available: since V0.9

.. contents::
   :depth: 2


============
Introduction
============

dijit._Templated is a mixin for most widgets in dijit. It takes an HTML template, and creates the widget's DOM tree according to that template. In other words, it implements buildRendering() for you.

Note that the underscore in the name implies not that _Template is a private class, but rather that it's a mixin, rather than a widget.


=====
Usage
=====

Mixin dijit._Templated when you declare your widget:

.. code-block :: javascript
 :linenos:

 <script type="text/javascript">
   dojo.declare("MyWidget", [dijit._Widget, dijit._Templated], {
       templateString: "<div>hello world</div>"
   });
 </script>

and then instead of defining buildRendering(), define a ``templateString``.


============
The template
============

The template is specified in the widget attribute ``templateString``, and points to some HTML w/a `single root node`, with special attributes on the tags, plus possibly substitution variables, etc.

It can either be specified as a literal string:

.. code-block :: javascript
 :linenos:

 <script type="text/javascript">
   dojo.declare("MyWidget", [dijit._Widget, dijit._Templated], {
       templateString: "<div>hello world</div>"
   });
 </script>


or pulled in from a file using `dojo.cache() <dojo/cache>`_

.. code-block :: javascript
 :linenos:

 <script type="text/javascript">
   dojo.declare("MyWidget", [dijit._Widget, dijit._Templated], {
       templateString: dojo.cache("myNameSpace", "templates/MyWidget.html"),
   });
 </script>

When using a built or released Dijit tree, the build will ``internStrings``, converting the dojo.cache() call into a literal string, avoiding a network request when users load the widget.

The tags in the template can have these special attributes, in addition to typical attributes like class:

  * data-dojo-attach-point
  * data-dojo-attach-event
  * role
  * aria-*

data-dojo-attach-point
----------------------
(before dojo 1.6 a.k.a. dojoAttachPoint)

In the JavaScript of a widget, you often might wish to refer to some of its html template's dom nodes directly. In this case the widget will need to access the <span> with the count in order to change the value.

You might think the widget author could just use ids in the html template, and then dojo.byId() in the widget's js. But if she does, then if two or more widget instances are created, they'll all have the same ids!  Obviously code will blow up then.

Instead, you the widget author do the following:

1. In your widget template's html, for every node that these variables are supposed to correspond to (eg point to), you add the attribute: data-dojo-attach-point="yourVariableNameHere".

2. In your widget's js, you use (without declaring them) variables for these nodes. In this case you will access this.counter.

The reason the variables are undeclared is that when the code in _Templated scans the html in step 1, and it finds the variables in the data-dojo-attach-point attribute, it adds those variables to your widget class, dynamically.

When using the ``widgetsInTemplate`` parameter, a data-dojo-attach-point on the widget node in the template will refer to the widget instance rather than the Dom Node.

data-dojo-attach-event
----------------------
(before dojo 1.6 a.k.a. dojoAttachEvent)

data-dojo-attach-event will automatically setup a connection from an event on the DOM node (onclick in this case) to call a method in the widget (in this case increment().

Here's an example of data-dojo-attach-point and data-dojo-attach-event:

.. code-example::
  :djConfig: parseOnLoad: false
  :type: inline
  :width: 400
  :height: 250
  :toolbar: versions, dir

  .. javascript::

	<script type="text/javascript">
		dojo.require("dijit._Widget");
		dojo.require("dijit._Templated");
		dojo.require("dojo.parser");

                dojo.addOnLoad(function(){
                dojo.declare("FancyCounter",
			[dijit._Widget, dijit._Templated], {
				// counter
				_i: 0,

				templateString:
					"<div>" +
						"<button dojoAttachEvent='onclick: increment'>press me</button>" +
						"&nbsp; count: <span dojoAttachPoint='counter'>0</span>" +
					"</div>",

				 increment: function(evt){
				 	this.counter.innerHTML = ++this._i;
				 }
			});
                        dojo.parser.parse();
                });
        </script>

  .. html::

	<span dojoType="FancyCounter">press me</span>


role and aria-*
---------------

(Before Dojo Toolkit v1.6 there were waiRole and waiState.)

These attributes are for accessibility, and define the role of DOM nodes such as "tree". See `Creating Accessible Widgets <quickstart/writingWidgets/a11y>`_ for more information.


containerNode
-------------

Often a widget declared in markup will have contents, i.e. it will contain some other DOM. For example:

.. code-block:: html

  <button dojoType="dijit.form.Button">press me</button>

If the template defines data-dojo-attach-point="containerNode", the children from the srcNodeRef will be copied to this node.

For example:

.. code-example::
  :djConfig: parseOnLoad: false
  :width: 400
  :height: 250
  :toolbar: versions, dir

  .. javascript::

    <script>
		dojo.require("dijit._Widget");
		dojo.require("dijit._Templated");
		dojo.require("dojo.parser");

                dojo.addOnLoad(function(){
		        dojo.declare("MyButton",
			[dijit._Widget, dijit._Templated], {
				templateString:
				    "<button dojoAttachPoint='containerNode' dojoAttachEvent='onclick: onClick'></button>",
                                onClick: function(evt){
                                        alert("Awesome!!");
                                }
			});
                        dojo.parser.parse();
                });
    </script>

  .. html::

	<button dojoType="MyButton">press me</button>

Substitution variables
----------------------

A template can also reference substitution variables like ${title}. ${title} references the title attribute of the widget.

However, this is not recommended, as (due to implementation details) it only handles setting of the title on widget instantiation. In other words, myWidget.attr('title', 'My new title') won't work if you use substitution variables.

See the section on attributeMap in `Writing Widgets <quickstart/writingWidgets>`_ for an alternative to substitution variables.


===========================
Widgets inside the Template
===========================

So what if we want the widget to have a widget inside of the template, as in ...:

.. code-block :: html

  <div class="combinedDateTime">
     <div dojoType="dijit.form.DateTextBox"></div>
     <div dojoType="dijit.form.TimeTextBox"></div>
  </div>

When using this template in a directly extended widget class, you will need to set the property widgetsInTemplate: true. Why? Because a widget inside a template requires some recursive parsing, which may be slow if you're drawing thousands of widgets ... especially if there is nothing extra to parse. Therefore, it is false by default.

dijit.Declaration-based widget classes automatically set widgetsInTemplate to true.

data-dojo-attach-point
----------------------

In this case, the data-dojo-attach-point becomes a pointer to the sub-widget, not to a DOM node. For example, with this template:

.. code-block :: html

  <div class="combinedDateTime">
     <div dojoType="dijit.form.DateTextBox" data-dojo-attach-point="start"></div>
     <div dojoType="dijit.form.TimeTextBox" data-dojo-attach-point="end"></div>
  </div>

You can do this in your widget code:

.. code-block :: javascript

  this.start.attr('value', new Date());


data-dojo-attach-event
----------------------

data-dojo-attach-event also functions to attach a widget event (not a DOM event) on the sub widget to the main widget. For example, consider InlineEditBox which embeds dijit buttons into it's own template:

.. code-block :: html

  <fieldset data-dojo-attach-point="editNode" role="presentation" style="position: absolute; visibility:hidden" class="dijitReset dijitInline"
	data-dojo-attach-event="onkeypress: _onKeyPress"
	><div data-dojo-attach-point="editorPlaceholder"></div
	><span data-dojo-attach-point="buttonContainer"
		><button class='saveButton' data-dojo-attach-point="saveButton" dojoType="dijit.form.Button" data-dojo-attach-event="onClick:save" disabled="true">${buttonSave}</button
		><button class='cancelButton' data-dojo-attach-point="cancelButton" dojoType="dijit.form.Button" data-dojo-attach-event="onClick:cancel">${buttonCancel}</button
	></span
  ></fieldset>

The onClick event on the dijit.form.Button will call InlineEditBox.save().


The widgetsInTemplate feature does not support adding layout widgets as children. In particular there are issues with startup() and resize() calls to the children.

Also note that a widget's getChildren() method and similar methods will *not* include the widgets declared in the template, but rather just the widgets inside the containerNode. This is because the widgets declared in the template are internal objects, effectively hidden from widget users. In other words, only the developer of the widget knows that it internally contains widgets.


===============
Common Pitfalls
===============

1. Be sure to only have one root node in your template

2. Don't start your template (or end it) with a comment (because that means you technically have two nodes)

3. Avoid a trailing </div> at the end of your template

4. For widgetsInTemplate, don't try to make the root node itself a widget. That's not supported (that would make the top node the root of two separate widgets and we can't support that).


========
See also
========

* `Writing Widgets <quickstart/writingWidgets>`_
