## page was renamed from 1.2/dojo
#format dojo_rst

Dojo
====

.. contents::
   :depth: 2

Dojo is divided into two parts: ``dojo.js``, and the rest of Dojo Core. Typically, if a function or Class exists within the dojo namespace directly (eg: ``dojo.require()``, ``dojo.addOnLoad()``) it is provided directly by ``dojo.js``. If the function or Class exists beneath the dojo namespace (eg: ``dojo.dnd.Mover``), you will need to require the appropriate module (eg: ``dojo.require("dojo.dnd.Mover");``)

These pages cover both cases, and indicate how they are provided.

==================
Base Dojo: dojo.js
==================

Dojo Base is the functionality you get by just including a stock built dojo.js or dojo.xd.js in your page.

Configuring Dojo (dojo/_base/config)
------------------------------------

* `dojoConfig (dojo/_base/config) <dojo/config>`_

  Possibility to override certain global settings that control how the framework operates

Array utilities
---------------

Details on dojo.every, dojo.filter, dojo.forEach, dojo.indexOf, dojo.lastIndexOf, dojo.map, and dojo.some. See the `Array QuickStart <quickstart/arrays>`_ for an overview.

* `dojo.forEach <dojo/forEach>`_

  Invokes a callback function for every item in array

* `dojo.map <dojo/map>`_

  Applies a callback to each element of arr and returns an Array with the results

* `dojo.some <dojo/some>`_

  Iterate over an array, escaping when the callback returns true for some logic check.

* `dojo.every <dojo/every>`_

  Iterate over an array, escaping when the callback returns false for some logic check.

* `dojo.filter <dojo/filter>`_

  Iterate over an array, reducing the array based on the callback return.

* `dojo.indexOf <dojo/indexOf>`_

  Find the index of some element in an Array.

* `NodeList array methods <dojo/NodeList#array>`_

  * NodeList.indexOf, NodeList.lastIndexOf, NodeList.forEach, NodeList.every, NodeList.some, NodeList.concat, NodeList.map, NodeList.filter, NodeList.at

Language Utilities
------------------


* `dojo.hitch <dojo/hitch>`_

  Function that generates a wrapper function that ensures a function that will only ever execute in a defined scope.

* `dojo.partial <dojo/partial>`_

  Function that generates a wrapper function that ensures a function will only ever execute globally.

* `dojo.delegate <dojo/delegate>`_

  Returns a new object which "looks" to obj for properties which it does not have a value for.

* `dojo.isString <dojo/isString>`_

  Checks if the parameter is a String

* `dojo.isArray <dojo/isArray>`_

  Checks if the parameter is an Array

* `dojo.isFunction <dojo/isFunction>`_

  Checks if the parameter is a Function

* `dojo.isObject <dojo/isObject>`_

  Checks if the parameter is an Object

* `dojo.isArrayLike <dojo/isArrayLike>`_

  Checks if the parameter is like an Array

* `dojo.isAlien <dojo/isAlien>`_

  Checks if the parameter is a built-in function


String Utilities
----------------

* `dojo.trim <dojo/trim>`_

  Trim whitespace from a String

* `dojo.replace <dojo/replace>`_

  Simple templates with parameterized substitutions.

DOM (dojo/dom)
--------------

from 1.7 + dojo/dom module collects following part of dojo APIs

* `dojo.query <dojo/query>`_

  The swiss army knife of DOM node manipulation in Dojo.

* `dojo.NodeList <dojo/NodeList>`_

  A class to handle a list of DOM nodes. Most commonly returned from a `dojo.query` call.

* `dojo.byId <dojo/byId>`_

  Select a DOM node by 'id'.

* dojo.isDescendant

* dojo.setSelectable

* Manipulation (dojo/dom-construct)

  * dojo.toDom

    Instantiates an HTML fragment returning the corresponding DOM.

  * `dojo.create <dojo/create>`_

    Creates a dom node with optional values and placement

  * `dojo.place <dojo/place>`_

    Place DOM nodes relative to others

  * `dojo.destroy <dojo/destroy>`_

    Destroy a DOM element

  * `dojo.empty <dojo/empty>`_

    Empty the contents of a DOM element


* Attributes (dojo/dom-attr)

  * `dojo.attr <dojo/attr>`_

    Modifying DOM node attributes

  * `dojo.getAttr <dojo/getAttr>`_

    Gets an attribute on an HTML element.

  * `dojo.setAttr <dojo/setAttr>`_

    Sets an attribute on an HTML element.

  * `dojo.hasAttr <dojo/hasAttr>`_

    Returns true if the requested attribute is specified on the given element, and false otherwise.

  * `dojo.removeAttr <dojo/removeAttr>`_

    Removes an attribute from an HTML element.

  * `dojo.getNodeProp <dojo/getNodeProp>`_

    Returns an effective value of a property or an attribute.

* Form (dojo/dom-form)

  * `dojo.fieldToObject <dojo/fieldToObject>`_

    Serialize a form field to a JavaScript object.

  * `dojo.formToJson <dojo/formToJson>`_

    Create an object from an form node

  * `dojo.formToObject <dojo/formToObject>`_

    Serialize a form node to a JavaScript object.

  * `dojo.formToQuery <dojo/formToQuery>`_

    Returns a URL-encoded string representing the form passed as either a node or string ID identifying the form to serialize

* Styles (dojo/dom-style)

  * `dojo.style <dojo/style>`_

    A getter/setter for styles on a DOM node

  * `dojo.getComputedStyle <dojo/getComputedStyle>`_

    Return a cachable object of all computed styles for a node

  * `dojo.getStyle <dojo/getStyle>`_

    Accesses styles on a node.

  * `dojo.setStyle <dojo/setStyle>`_

    Sets styles on a node.

* Class (dojo/dom-class)

  * `dojo.hasClass <dojo/hasClass>`_

    Returns a boolean depending on whether or not a node has a passed class string.

  * `dojo.addClass <dojo/addClass>`_

    Adds a CSS class to a node.

  * `dojo.removeClass <dojo/removeClass>`_

    Removes a class from a Node.

  * `dojo.toggleClass <dojo/toggleClass>`_

    Toggles a className (or now in 1.4 an array of classNames).

  * dojo.replaceClass <dojo/replaceClass>`_

    Replaces one or more classes on a node if not present. Operates more quickly than calling dojo.removeClass and dojo.addClass 

* Geometry (dojo/dom-geometry)

  * `dojo.coords <dojo/coords>`_

    Getter for the coordinates (relative to parent and absolute) of a DOM node.  Deprecated in Dojo 1.4.

  * `dojo.position <dojo/position>`_

    Getter for the border-box x/y coordinates and size of a DOM node.
  
  * `dojo.marginBox <dojo/marginBox>`_

    Getter/setter for the margin-box of node

  * `dojo.contentBox <dojo/contentBox>`_

    Getter/setter for the content-box of node

Deferred Utility (dojo/_base/Deferred)
--------------------------------------
* `dojo.Deferred <dojo/Deferred>`_

  Communication between asynchronous calls



Window (dojo/_base/window)
--------------------------

from 1.7 + dojo/_base/window module collects following part of dojo APIs

* `dojo.doc <dojo/doc>`_

  Alias for the current document.

* `dojo.body <dojo/body>`_

  Return the body element of the document

* `dojo.setContext <dojo/setContext>`_

  Changes the behavior of many core Dojo functions that deal with namespace and DOM lookup

* `dojo.withGlobal <dojo/withGlobal>`_

  Call callback with globalObject as dojo.global and globalObject.document as dojo.doc

* `dojo.withDoc <dojo/withDoc>`_

  Call callback with documentObject as dojo.doc

Effects
-------

* `dojo.animateProperty <dojo/animateProperty>`_

  The workhorse of most `dojo.fx <dojo/fx>`_ animations. Used for animating CSS properties

* `dojo.Animation <dojo/Animation>`_

  **1.4+** previously dojo._Animation, the class behind all dojo.fx

* `dojo.anim <dojo/anim>`_

  Shorthand version of animateProperty using positional arguments

* `dojo.fadeOut <dojo/fadeOut>`_

* `dojo.fadeIn <dojo/fadeIn>`_

Events
------

* `dojo.connect <dojo/connect>`_

  Connects events to methods

* `NodeList.connect <dojo/NodeList#connect>`_

  Connects events to every node in the list, like dojo.connect

* `NodeList.events <dojo/NodeList#events>`_

  Common event names mapped as functions on a NodeList - eg: .onclick(function(){})

* `dojo.disconnect <dojo/disconnect>`_

  Disconnects methods from linked topics

* `dojo.subscribe <dojo/subscribe>`_

  Linked a listener to a named topic

* `dojo.unsubscribe <dojo/unsubscribe>`_

  Remove a topic listener

* `dojo.publish <dojo/publish>`_

  Publish an event to all subscribers of a topic

* `dojo.connectPublisher <dojo/connectPublisher>`_

  Ensure that everytime an event is called, a message is published on the topic.

* `dojo.stopEvent <dojo/stopEvent>`_

  Stop an event's bubbling and propagation.


Document Lifecycle
------------------

* `dojo.addOnLoad <dojo/addOnLoad>`_

  Call functions after the DOM has finished loading and widgets declared in markup have been instantiated

* `dojo.ready <dojo/ready>`_

  **1.4+** Alias for `dojo.addOnLoad <dojo/addOnLoad>`_

* `dojo.addOnUnload <dojo/addOnUnload>`_

  Call functions when the page unloads

* `dojo.addOnWindowUnload <dojo/addOnWindowUnload>`_

  Call functions when window.onunload fires

* `dojo.windowUnloaded <dojo/windowUnloaded>`_

  Signal fired by impending window destruction

Ajax / IO
---------

* `IO Pipeline Topics <dojo/ioPipelineTopics>`_

* `dojo.contentHandlers <dojo/contentHandlers>`_

  **1.4+** Pre-defined XHR content handlers, and an extension point to add your own custom handling.

* `dojo.xhr <dojo/xhr>`_

  Core for all xhr* verbs, eg: xhrPost, getGet

* `dojo.xhrDelete <dojo/xhrDelete>`_

* `dojo.xhrGet <dojo/xhrGet>`_

* `dojo.xhrPost <dojo/xhrPost>`_

* `dojo.xhrPut <dojo/xhrPut>`_

* `dojo.rawXhrPost <dojo/rawXhrPost>`_

* `dojo.rawXhrPut <dojo/rawXhrPut>`_

Package System
--------------

* `dojo.registerModulePath <dojo/registerModulePath>`_

  Maps module name to a path

* `dojo.require <dojo/require>`_

  Loads a Javascript module from the appropriate URI

* `dojo.provide <dojo/provide>`_

* `dojo.moduleUrl <dojo/moduleUrl>`_

JSON Tools
----------

* `dojo.fromJson <dojo/fromJson>`_

  Parses a JSON string to return a JavaScript object

* `dojo.toJson <dojo/toJson>`_

  Returns a JSON serialization of an object

Objects / OO Tools
------------------

* `dojo.mixin <dojo/mixin>`_

  Mixes one object into another. Can be used as a shallow copy

* `dojo.declare <dojo/declare>`_

  Creates a constructor using a compact notation for inheritance and prototype extension

* `dojo.extend <dojo/extend>`_

* `dojo.exists <dojo/exists>`_

  Determine if an object supports a given method

* `dojo.delegate <dojo/delegate>`_

  Delegate an Object (beget)

* `dojo.getObject <dojo/getObject>`_

  Get a property from a dot-separated string, such as "A.B.C"

* `dojo.setObject <dojo/setObject>`_

  Set a property from a dot-separated string, such as "A.B.C"

* `dojo.objectToQuery <dojo/objectToQuery>`_

* `dojo.queryToObject <dojo/queryToObject>`_

* `NodeList.instantiate <dojo/NodeList#instantiate>`_

  Create classes out of each node in the list


Colors
------

* `dojo._base.Color <dojo/_base/Color>`_

  Color object and utility functions to handle colors.
  Details on

* dojo.colorFromArray

* dojo.colorFromHex

* dojo.colorFromString

* dojo.colorFromRgb.


Miscellaneous Base
------------------

* `dojo.deprecated <dojo/deprecated>`_

  Log a debug message to indicate that a behavior has been deprecated

* `dojo.eval <dojo/eval>`_

  Evaluate some string of JavaScript

* `dojo.global <dojo/global>`_

  Alias for the global scope

* `dojo.keys <dojo/keys>`_

  A collection of key constants.

* `dojo.locale <dojo/locale>`_

  A string containing the current locale as defined by Dojo

* `dojo.version <dojo/version>`_

  The current version number of Dojo

* `dojo._Url <dojo/Url>`_

  dojo._Url is used to manage the url object.


=========
Dojo Core
=========

* `dojo.AdapterRegistry <dojo/AdapterRegistry>`_

  A registry to make contextual calling/searching easier

* `dojo.back <dojo/back>`_

  Browser history management resources (Back button functionality)

* `dojo.behavior <dojo/behavior>`_

  Utility for unobtrusive/progressive event binding, DOM traversal, and manipulation

* `dojo.cldr <dojo/cldr>`_

  A Common Locale Data Repository (CLDR) implementation

* `dojo.cache <dojo/cache>`_

  **1.4+** A mechanism to cache inline text.

* `dojo.colors <dojo/colors>`_

  CSS color manipulation functions

* `dojo.cookie <dojo/cookie>`_

  Simple HTTP cookie manipulation

* `dojo.currency <dojo/currency>`_

  Localized formatting and parsing routines for currency data

* `dojo.data <dojo/data>`_

  A uniform data access layer

  * `dojo.data.api <dojo/data/api>`_

  * `dojo.data.api.Read <dojo/data/api/Read>`_

  * `dojo.data.api.Write <dojo/data/api/Write>`_

  * `dojo.data.api.Identity <dojo/data/api/Identity>`_

  * `dojo.data.api.Notification <dojo/data/api/Notification>`_

  * `dojo.data.ItemFileReadStore <dojo/data/ItemFileReadStore>`_

  * `dojo.data.ItemFileWriteStore <dojo/data/ItemFileWriteStore>`_

* `dojo.date <dojo/date>`_

  Date manipulation utilities

  * dojo.date.locale

    Offers a library of localization methods to format and parse dates and times

    * `dojo.date.locale.addCustomFormats <dojo/date/locale/addCustomFormats>`_

      Adds a reference to a bundle containing localized custom formats to be used by date/time formatting and parsing routines.

    * `dojo.date.locale.format <dojo/date/locale/format>`_

      Formats a Date object as a String, using locale-specific settings or custom patterns.

    * `dojo.date.locale.getNames <dojo/date/locale/getNames>`_

      Used to get localized strings from dojo.cldr for day or month names.

    * `dojo.date.locale.isWeekend <dojo/date/locale/isWeekend>`_

      Determines if the date falls on a weekend, according to local custom.

    * `dojo.date.locale.parse <dojo/date/locale/parse>`_

      Converts a properly formatted string to a primitive Date object, using locale-specific settings.

    * `dojo.date.locale.regexp <dojo/date/locale/regexp>`_

      Builds the regular needed to parse a localized date

* `dojo.DeferredList <dojo/DeferredList>`_

  Event handling for a group of Deferred objects

* `dojo.dnd <dojo/dnd>`_

  Drag and Drop

  * `dojo.dnd.Moveable <dojo/dnd/Moveable>`_

* `dojo.fx <dojo/fx>`_

  Effects library on top of Base animations

* `dojo.gears <dojo/gears>`_

  Google Gears

* `dojo.hash <dojo/hash>`_
 
  Normalized onhashchange module


* `dojo.html <dojo/html>`_

  Inserting contents in HTML nodes

* `dojo.i18n <dojo/i18n>`_

  Utility classes to enable loading of resources for internationalization

* Additional AJAX I/O transports (dojo.io)

  * `dojo.io.iframe <dojo/io/iframe>`_

    Sends an AJAX I/O call using an IFrame

  * `dojo.io.script <dojo/io/script>`_

    Sends a JSONP request using a script tag

* `dojo.jaxer <dojo/jaxer>`_

* `dojo.NodeList-data <dojo/NodeList-data>`_

  Adds a .data() and .removeData() API to `dojo.query <dojo/query>`_ operations

* `dojo.NodeList-fx <dojo/NodeList-fx>`_

  Adds dojo.fx animation support to dojo.query()

* `dojo.NodeList-html <dojo/NodeList-html>`_

  Adds a chainable html method to dojo.query()

* `dojo.NodeList-manipulate <dojo/NodeList-manipulate>`_

  **1.4+** Method extensions to dojo.NodeList/dojo.query() that manipulate HTML.

* `dojo.NodeList-traverse <dojo/NodeList-traverse>`_

  **1.4+** Method extensions to dojo.NodeList/dojo.query() for traversing the DOM.

* `dojo.number <dojo/number>`_

  Localized formatting and parsing methods for number data

* `dojo.parser <dojo/parser>`_

  The Dom/Widget parsing package

* `dojo.regexp <dojo/regexp>`_

  Regular expressions and Builder resources

* `dojo.robot <dojo/robot>`_

  experimental module for DOH users

* `dojo.robotx <dojo/robotx>`_

  experimental module for DOH users

* `dojo.rpc <dojo/rpc>`_

  Communicate via Remote Procedure Calls (RPC) with Backend Servers

  * `dojo.rpc.JsonpService <dojo/rpc/JsonpService>`_

    Generic JSONP service

  * `dojo.rpc.JsonService <dojo/rpc/JsonService>`_

    JSON RPC service

  * `dojo.rpc.RpcService <dojo/rpc/RpcService>`_

    RPC service class

* `dojo.store <dojo/store>`_

  **1.6+** Dojo Store is an uniform interface for the access and manipulation of stored data that will eventually replace `dojo.data <dojo/data>`_

  * `dojo.store.Memory <dojo/store/Memory>`_

    A data access interface for in memory storage

  * `dojo.store.JsonRest <dojo/store/JsonRest>`_

    A data access interface for a RESTful service providing JSON data

  * `dojo.store.Observable <dojo/store/Observable>`_

    A wrapper for data stores that are observable

  * `dojo.store.Cache <dojo/store/Cache>`_

    A wrapper for data stores that are cacheable

* `dojo.string <dojo/string>`_

  String utilities for Dojo


========
See also
========

* `Dijit <dijit/index>`__

  The widget system layered on top of Dojo

* `DojoX <dojox/index>`__

  An area for development of extensions to the Dojo toolkit
