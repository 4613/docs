## page was renamed from 1.2/dijit/layout/TabContainer
#format dojo_rst

dijit.layout.TabContainer
=========================

:Status: Contributed, Draft
:Version: 1.0

.. contents::
   :depth: 3

A TabContainer is a container that has multiple panes, but shows only one pane at a time. There are a set of tabs corresponding to each pane, where each tab has the title (aka label) of the pane, and optionally a close button. You can use tabs in your own application and style them as you want, but they also fit perfectly into the dijit.layout system. 

==============
Basic Examples
==============

First, We'll demonstrate a programatic TabContainer creation from existing markup.
Note that the tabs all have a fixed height.

.. cv-compound::
 
  As a simple example, we'll use `dojo.query <dojo/query>`_ to find and create the ContentPanes used in the TabContainer

  .. cv:: javascript

    <script type="text/javascript">
    dojo.require("dijit.layout.TabContainer");
    dojo.require("dijit.layout.ContentPane");
    dojo.addOnLoad(function(){
        dojo.query(".tc1cp").forEach(function(n){
            new dijit.layout.ContentPane({
                // just pass a title: attribute, this, we're stealing from the node
                title: dojo.attr(n,"title") 
            }, n);
        });
        var tc = new dijit.layout.TabContainer({
            style: dojo.attr("tc1-prog", "style") 
        },"tc1-prog");
        tc.startup(); 
    });
    </script>

  The html is very simple

  .. cv:: html

    <div id="tc1-prog" style="width: 100%; height: 100px;">
      <div class="tc1cp" title="My first tab">
        Lorem ipsum and all around...
      </div>
      <div class="tc1cp" title="My second tab">
        Lorem ipsum and all around - second...
      </div>
      <div class="tc1cp" title="My last tab">
        Lorem ipsum and all around - last...
      </div>
    </div>


The `parser </dojo/parser>`_ does a lot of the heavy lifting seen above in the programatic method, finding attributes on the node and passing them to the Widget being created. By using a dojoType to identify these nodes, our initial creation is very easy, as seen in the remainder of these examples: 

.. cv-compound::

  This is a plain TabContainer with three tabs and fixed height. The third tab is closable

  .. cv:: javascript

    <script type="text/javascript">
    dojo.require("dijit.layout.TabContainer");
    dojo.require("dijit.layout.ContentPane");
    </script>

  The html is very simple

  .. cv:: html

    <div dojoType="dijit.layout.TabContainer" style="width: 100%; height: 100px;">
      <div dojoType="dijit.layout.ContentPane" title="My first tab" selected="true">
        Lorem ipsum and all around...
      </div>
      <div dojoType="dijit.layout.ContentPane" title="My second tab">
        Lorem ipsum and all around - second...
      </div>
      <div dojoType="dijit.layout.ContentPane" title="My last tab" closable="true">
        Lorem ipsum and all around - last...
      </div>
    </div>

This is a plain TabContainer with three tabs and flexible height using the doLayout="false" attribute. The second tab is closable.

.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
    dojo.require("dijit.layout.TabContainer");
    dojo.require("dijit.layout.ContentPane");
    </script>

  The html is very simple

  .. cv :: html
    
    <!-- this div is only for documentation purpose, in real development environments, just take it out -->
    <div style="height: 100px;">

      <div dojoType="dijit.layout.TabContainer" style="width: 100%;" doLayout="false">
        <div dojoType="dijit.layout.ContentPane" title="My first tab" selected="true">
          Lorem ipsum and all around...
        </div>
        <div dojoType="dijit.layout.ContentPane" title="My second tab" closable="true">
          Lorem ipsum and all around - second...
          <br />
          Hmmm expanding tabs......
        </div>
        <div dojoType="dijit.layout.ContentPane" title="My last tab">
          Lorem ipsum and all around - last...
          <br />
          <br />
          <br />
          Hmmm even more expanding tabs......
        </div>
      </div>

    <!-- end of the div -->
    </div>

More examples
-------------

There are several more examples of basic use cases `available <TabContainer-examples>`_ 

Like `dijit.layout.StackContainer </dijit/layout/StackContainer>`_, TabContainer works by using a simple ``.addChild``, ``.removeChild``, and ``.selectChild`` API, all accepting a widget to be acted upon. 

Manipulating Children
---------------------

.. code-block :: javascript 
  :linenos:

  var tabs = dijit.byId("myTabContainer");
  var pane = new dijit.layout.ContentPane({ title:"Remote Content", href:"remote.html" });
  tabs.addChild(pane);

A Tab doesn't get displayed unless you call ``.selectChild``

.. code-block :: javascript 
  :linenos:

  var tabs = dijit.byId("myTabContainer");
  var pane = new dijit.layout.ContentPane({ title:"Remote Content", href:"remote.html" });
  tabs.addChild(pane);
  tabs.selectChild(pane);

the ``addChild`` method accepts a position index, telling where in the order to add the new pane:

.. code-block :: javascript 
  :linenos:

  var tabs = dijit.byId("myTabContainer");
  var pane = new dijit.layout.ContentPane({ title:"Remote Content", href:"remote.html" });
  tabs.addChild(pane,1);

This will add the new remote pane after the first pane (0).

Closing A Tab 
-------------

A common action for ``closable`` tabs is to register an ``onClose`` function on the child, returning true or false to indicate weather or not the closing should take place:

.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
    dojo.require("dijit.layout.TabContainer");
    dojo.require("dijit.layout.ContentPane");
    dojo.addOnLoad(function(){
        var tabs = dijit.byId("onClose-ex");
        var closablePane = new dijit.layout.ContentPane({
            title:"Close Me",
            closable: true, 
            onClose: function(){
               // confirm() returns true or false, so return that.
               return confirm("Do you really want to Close this?");
            }
        });
        tabs.addChild(closablePane);
    });
    </script>

  You can, of course, attach the onClose function directly on a pane as well:

  .. cv :: html
    
    <div style="height: 100px;">

      <div id="onClose-ex" dojoType="dijit.layout.TabContainer" style="width: 100%;" doLayout="false">
        <div dojoType="dijit.layout.ContentPane" title="My first tab" selected="true">
          Lorem ipsum and all around...
        </div>
        <div dojoType="dijit.layout.ContentPane" title="Other Closable" closable="true" onClose="return confirm('really?');">
            ... I have an in-line onClose
        </div>
      </div>

    </div>


TabContainer Events
-------------------

There are two methods of observing TabContainer *shenanigans*. The first, by using `dojo.subscribe </dojo/subscribe>`_. Each TabContainer `publishes </dojo/publish>`_ notices based on the *id* of the Container. Several different actions are tracked this way:

.. code-block :: javascript
  :linenos:

  // assuming our tabContainer has id="bar"
  dojo.subscribe("bar-selectChild", function(child){ 
      console.log("A new child was selected:", child); 
  });

  dojo.subscribe("bar-addChild", function(child){
      console.log("A child was added:", child);
  });

  dojo.subscribe("bar-removeChild", function(child){
      console.log("Child is gone: ", child); // but not destroyed!
  });

the -selectChild subscription will not execute if the selected child is already the visible Pane. It will only publish when a *different* child is selected. Notice how this differs from our other method of wiring up TabContainer events, via `dojo.connect </dojo/connect>`_:

.. code-block :: javascript
  :linenos:

  // assuming the same id="bar" TabContainer
  var tabs = dijit.byId("bar");
  
  dojo.connect(tabs,"selectChild",function(child){ 
      console.log("called anytime selectChild is");
  });
  dojo.connect(tabs,"addChild",function(child){
      console.log("just added: ", child);
  });


This simply uses dojo.connect to listen to the native function calls. 

A common request for ``selectChild`` functionality is to know both the *new* and *old* widgets being transitioned. The easiest way to accomplish this is connect to the "private" ``_transition`` method of a TabContainer:

.. code-block :: javascript
  :linenos:

  var tabs = dijit.byId("tabs");
  dojo.connect(tabs,"_transition", function(newPage, oldPage){ 
      console.log("I was showing: ", oldPage || "nothing");
      console.log("I am now showing: ", newPage);
  });

It is worth noting: If you need a function to be called *absolutely every* time a child is added to a TabContainer (or StackContainer), you need to listen to the ``_setupChild`` function to ensure you are notified of the children already existing in markup. This is only relevant if you are subclassing for reason:

.. code-block :: javascript
  :linenos:
 
  dojo.declare("my.TabContainer", dijit.layout.TabContainer, {
      _setupChild: function(child){ 
           this.inherited(arguments);
           console.log("I've seen: ", child);
      }
  });
  
This is because ``addChild`` will not be called for existing panes (in markup).

 
