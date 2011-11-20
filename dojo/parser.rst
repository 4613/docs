#format dojo_rst

The Dojo Parser
===============

:Status: Contributed
:Version: 1.7
:Authors: Peter Higgins, Nathan Toone, Bill Keese, kolban

.. contents::
    :depth: 3

The Dojo Parser is an optional module which is used to convert specially decorated nodes in the DOM and convert them into `Dijits <dijit/index>`_. By `decorated` we mean use of a `data-dojo-type` (dojoType) attribute. Any "Class" (or object, such as the ones created by `dojo.declare <dojo/declare>`_) can be instantiated by using a `data-dojo-type` attribute on some node in the DOM, and create a widget out of it.

This is not limited to Dijit, or `dojo.declare <dojo/declare>`_. 

Inside your HTML you mark nodes for the parser by setting the data-dojo-type attribute, to specify the class of the widget, and other attributes, to specify parameters to the widget.   For example:

.. code-block :: html

  <input data-dojo-type="dijit.form.TextBox" name="nm" value="hello world">


The parser can scan the entire DOM for ``data-dojo-type`` attributes, and create new instances from nodes like this.

The parser also allows function parameters and connections to be done via <script> tags, for example:

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/connect" data-dojo-event="functionToConnectTo">
           console.log("I will execute in addition to functionToConnectTo().");
        </script>
    </div>


Getting Started
---------------

==================
Loading the Parser
==================

To include the Dojo parser on your page, require the module `dojo.parser`:

.. code-block :: javascript

  dojo.require("dojo.parser");

``note:`` dijit._Templated require()'s dojo.parser, so a lot of examples don't include this step (dijit._Templated is loaded by most every Dijit). It is always safer to explicitly `require <dojo/require>`_ the module than to assume it has been loaded.

Also, starting in 1.7, many widgets extend `dijit._TemplatedMixin <dijit/_TemplatedMixin>` rather than `dijit._Templated <dijit/_Templated>`, so the parser isn't included in that case.

==================
Running the Parser
==================

There are two ways to run the dojo.parser: manually, or before onLoad.

To execute the parser manually, simply call the function ``parse``:

.. code-block :: javascript
  
  dojo.parser.parse();

To run the parser when your page loads, add a data-dojo-config="parseOnLoad: true" to your dojo script tag:

.. code-block :: html

		<script type="text/javascript" src="dojo/dojo.js"
			data-dojo-config="parseOnLoad: true"></script>



Parser syntax
-------------

=====================
Specifying parameters
=====================

Attributes which correspond to native HTML attributes appear directly in the markup.    Custom widget parameters are put into the data-dojo-props field.   For example:

.. code-block :: html

       <input data-dojo-type="dijit.form.TextBox" name="dept"
            data-dojo-props="scrollOnFocus: true"/>


==================
Boolean parameters
==================

Due to HTML subtleties, for boolean parameters that are false, it's best not to specify the attribute at all.   For example, to specify an enabled button (where the `disabled` property is false), simply don't specify anything for disabled:

.. code-block :: html

  <input data-dojo-type="dijit.form.Button">

Further, in standard HTML (as opposed to XHTML), the special parameters `checked` and `disabled` and `selected` should be specified as single keywords without a value:

.. code-block :: html

  <input data-dojo-type="dijit.form.Button" disabled>
  <input data-dojo-type="dijit.form.CheckBox" checked>

In XHTML they should be specified in the official format of repeating the attribute name as the value:

.. code-block :: html

  <input data-dojo-type="dijit.form.Button" disabled="disabled"/>
  <input data-dojo-type="dijit.form.CheckBox" checked="checked"/>

Although specifying disabled="true" will disable a widget, note that the following syntax should not be used as it's unreliable whether it evaluates to true or false:

.. code-block :: html

  <input data-dojo-type="dijit.form.Button" disabled=""/>


===============
Date parameters
===============
* Regardless of the locale of the client or server, dates are specified to the parser in ISO format:

.. code-block :: html

  <div data-dojo-type=... when="2009-1-31"></div>

Incidentally, this is also how dates are returned to the server when a form is submitted.


* To specify a value as today's date (or the current time, when specifying a time), use the keyword "now":

.. code-block :: html

  <div data-dojo-type=... when="now"></div>

===================
Function parameters
===================
There are two ways to specify a function parameter to a widget, either via an attribute or a script tag (see below).   To specify a function as an attribute you can either specify the name of a function:

.. code-block :: html

  <script>
     function myOnClick(){ ... }
  </script>
  <div data-dojo-type=... onClick="myOnClick"></div>


Alternately, you can inline the text of a function:

.. code-block :: html

  <div data-dojo-type=... onClick="alert('I was clicked');"></div>


===========
Script Tags
===========
The parser allows the specification of behaviours through custom types in script blocks to extend and enhance the functionality of declarative widgets. This is done by specifying a script block that is a direct child of a node with decorate with `data-dojo-type`. There are different types of script tags supported:

Connecting to a Function
~~~~~~~~~~~~~~~~~~~~~~~~

To perform a ``dojo.connect()`` on a method in a widget, use ``type="dojo/connect"`` inside a script node:

.. code-block :: html

    <div data-dojo-type="someType">
        <script type="dojo/connect" data-dojo-event="methodOfSomeType">
           console.log("I will execute in addition to methodOfSomeType().");
        </script>
    </div>

Override a Function
~~~~~~~~~~~~~~~~~~~

Sometimes you need to override a function in a widget.   Most commonly that happens when you need to specify a function that returns a value. (The value returned from ``dojo.connect()``'d functions is ignored.)

In that case use the ``type="dojo/method"`` syntax:

.. code-block :: html

    <div data-dojo-type="someType">
        <script type="dojo/method" data-dojo-event="methodOfSomeType">
           console.log("I will execute instead of methodOfSomeType().");
        </script>
    </div>


Execute Code on Instantiation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To execute code on instantiation, use the same format but don't specify an event flag:

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/method">
           console.log("I will execute on instantiation");
        </script>
    </div>


Execute Code on Change of Property
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**New in 1.7** To execute code when a value changes for a property for objects that support ``object.watch()`` the ``type="dojo/watch"`` can be used:

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/watch" data-dojo-prop="value" data-dojo-args="prop,oldValue,newValue">
           console.log("Property '"+prop+"' changed from '"+oldValue+"' to '"+newValue+"'");
        </script>
    </div>


The ``.watch()`` function always passes three arguments when it is called, representing the property that change, the old value and then the new value.

**Note** because ``data-dojo-prop`` attribute was introduced after the attribute changes of 1.6, there is no backwards support for just ``prop`` as an attribute.

Execute Code when an Event Occurs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**New in 1.7** While similar to ``dojo.connect()``, the ``type="dojo/on"`` can be used to specify ``on`` behaviour:

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/on" data-dojo-event="click" data-dojo-args="e">
           console.log("I was clicked!");
        </script>
    </div>


Arguments
~~~~~~~~~

For functions that take (named) parameters, specify them in an `data-dojo-args` attribute.  For example, onChange() gets a value parameter, so to reference it do:

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/connect" data-dojo-event="onChange" data-dojo-args="value">
           console.log("new value is " + value);
        </script>
    </div>

`data-dojo-args` is a comma separated list of parameter names. This example overrides TreeStoreModel's method getChildren:

.. code-block :: html

    <div data-dojo-type="dijit.tree.TreeStoreModel" store="store">
        <script type="dojo/method" data-dojo-event="getChildren" data-dojo-args="item, onComplete">
            return store.fetch({query: {parent: store.getIdentity(item)}, onComplete: onComplete});
        </script>
    </div>

Script Scope
~~~~~~~~~~~~

Note that `this` points to the widget object.

.. code-block :: html

    <div data-dojo-type=...>
        <script type="dojo/connect" data-dojo-event="onChange" data-dojo-args="value">
           console.log("onChange for " + this.id);
        </script>
    </div>



Writing widgets
---------------

This section discusses how to write widgets that the parser can understand.

===============================
Specifying parameters and types
===============================

HTML sets all attributes on nodes as strings.  However, when the parser instantiates your nodes, it looks at the prototype of the class you are trying to instantiate (via data-dojo-type attribute) and trys to make a "best guess" at what type your value should be.  This requires that all attributes you want to be passed in via the parser have a corresponding attribute in the class you are trying to instantiate.

Private members (those that begin with an underscore (_) ) are not mapped in from the source node.

For example, given the class:

.. code-block :: javascript

  dojo.declare("my.custom.type", null, {
    name: "default value",
    value: 0,
    when: new Date(),
    objectVal: null,
    anotherObject: null,
    arrayVal: [],
    typedArray: null,
    _privateVal: 0
  });

And HTML node:

.. code-block :: html

  <div data-dojo-type="my.custom.type" name="nm" value="5" when="2008-1-1" objectVal="{a: 1, b:'c'}" 
         anotherObject="namedObj" arrayVal="a,b,c,1,2" typedArray="['a','b','c',1,2]"
         _privateVal="5" anotherValue="more"></div>

The parser would create an object and pass it paramaters of:

.. code-block :: javascript

  {
    name: "nm",                                 // Just a simple string
    value: 5,                                   // Typed to an integer
    when: dojo.date.stamp.fromISOString("2008-1-1"); // Typed to a date
    objectVal: {a: 1, b:'c'},                   // Typed to an object
    anotherObject: dojo.getObject("namedObj"),  // For strings, try getting the object via dojo.getObject
    arrayVal: ["a","b","c","1","2"],            // When typing to an array, all entries are strings
    typedArray: ["a", "b", "c", 1, 2]           // To get a "typed" array, treat it like an object instead
  }

Note that _privateVal is not passed in (since it is private), and anotherValue is not passed in either (since it does not exist in the prototype of the class).

The parser automatically will call the startup() function of all nodes when it is finished parsing (if the function exists, ie for dijit widgets)

If you don't want to set a default value for an attribute, you can give it an empty value in your prototype.  Empty values of types are as follows:

  * NaN = an integer
  * "" = a string
  * null = an object
  * [] = an array
  * function(){} = a function
  * new Date("") = a date/time


=============
markupFactory
=============

As listed above, the parser expects widget constructors to follow a certain format (where the first argument is a hash of attribute names/values, and the second is the srcNodeRef.

If you are retrofitting an existing class to work with the parser, and the constructor does not follow this format, simply create a markupFactory method (a static method) which takes those two parameters and creates a new instance of the widget:

.. code-block :: javascript

   markupFactory: function(params, srcNodeRef){
        ...
        return newWidget;
   }

In addition the markupFactory can be used to allow the widget to do something that the parser doesn't automatically support, like the parsing of child nodes of the main node.  The developer can then adjust the initialisation parameters of the widget and pass those to the constructor.  The parser passes the class constructor as the third argument when it invokes the markupFactory.  For example:

.. code-block :: javascript

     markupFactory: function(params, srcNodeRef, ctor) {
       ...
       return new ctor(params, srcNodeRef);
     }

This also ensures that subsequent descendent classes that do not override the markupFactory are created properly.

Setting the parser behavior
---------------------------

``todoc: parseOnLoad`` parseOnLoad:false by default, parseOnLoad:true optional, parseOnLoad:true makes addOnLoad call after parsing. howto set parseOnLoad

``NEW in 1.3:``  Beginning in release 1.3 of dojo, you can manually call dojo.parser.instantiate on any node - and pass in an additional mixin to specify options, such as dojoType, etc.  The values in the mixin would override any values in your node. For example:

.. code-block :: html

  <div id="myDiv" name="ABC" value="1"></div>

You can manually call the parser's instantiate function (which does the "Magical Typing") by doing:

.. code-block :: javascript

  dojo.parser.instantiate([dojo.byId("myDiv")], {dojoType: "my.custom.type"});

Calling instantiate in this way will return to you a list of instances that were created.  Note that the first parameter to instantiate is an array of nodes...even if it's one-element you need to wrap it in an array

``NEW in 1.4:``  You specify that you do not want subwidgets to be started if you pass _started: false in your mixin.  For example:

.. code-block :: javascript

  dojo.parser.instantiate([dojo.byId("myDiv")], {dojoType: "my.custom.type", _started: false});

``NEW in 1.6:``  Dojo V1.6 started to use data-dojo-type html5 attribute instead of dojoType. When using new data-dojo-type attribute other attributes must be put in data-dojo-props attribute because of performance improvement like so:

.. code-block :: html

  <a href="document.html"
     data-dojo-type="my.custom.type"
     data-dojo-props="href: 'document.html', 
       title: 'Lorem ipsum',
       objectVal:{a: 1, b:'c'},
       typedArray:['a','b','c',1,2],
       unstandardAttr: 'value'"
     title="Lorem ipsum">Lorem ipsum link</a>

``NEW in 1.7:`` Since data-dojo-props leads to duplication, there is again possible to use both data-dojo-props attribute like in 1.6 in addition to node attributes:

.. code-block :: html

  <a href="document.html"
     data-dojo-type="my.custom.type"
     data-dojo-props="objectVal:{a: 1, b:'c'},
       typedArray:['a','b','c',1,2]"
     title="Lorem ipsum" unstandardAttr="value">Lorem ipsum link</a>

``todoc: scoping a parser call to node by stringId|domNode``


Caveats
-------
``todoc: re-parsing, duplicate id's``

Examples
--------

Load some HTML content from a `remote URL <quickstart/ajax>`_, and convert the nodes decorated with ``data-dojo-type``'s into widgets:

.. code-block :: javascript

  dojo.xhrGet({
    url: "widgets.html",
    load: function(data){
        dojo.byId("container").innerHTML = data;
        dojo.parser.parse("container");
    }
  });

Delay page-level parsing until after some custom code (having set parseOnLoad:false):

.. code-block :: javascript

  dojo.require("dojo.parser");
  dojo.addOnLoad(function(){
       // do something();
       dojo.parser.parse();
  });



See Also
--------

- `Introduction to the Parser <http://dojocampus.org/content/2008/03/08/the-dojo-parser/>`_
