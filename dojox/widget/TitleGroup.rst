#format dojo_rst

dojox.widget.TitleGroup
=======================

:since: 1.6.0
:author: dante

A container widget which delegates a connection between children `TitlePanes <dijit/TitlePane>`_. Behaves similarly to an `AccordionContainer <dijit/layout/AccordionContainer>`_ though has a variable overall height and does not "dock" to other layout widgets, such as a `BorderContainer <dijit/layout/BorderContainer>`_. 

Examples
========

A simple declarative example:

.. code-example::

  .. css::

     <style type="text/css"> 
        @import "{{baseUrl}}dojox/widget/TitleGroup/TitleGroup.css";
     </style>

  .. javascript::

    <script>
        dojo.require("dojox.widget.TitleGroup");
        dojo.require("dijit.TitlePane");
        dojo.require("dijit.form.Button");
    </script>

  .. html::

    <h2>Content before</h2>
    <div id="titleGroupA" data-dojo-type="dojox.widget.TitleGroup">
        <div dojoType="dijit.TitlePane" open="true" title="Pane 1">Lorem</div>
        <div dojoType="dijit.TitlePane" open="false" title="Pane 2">Lorem <br> <div data-dojo-type="dijit.form.Button">click</div></div>
        <div dojoType="dijit.TitlePane" open="false" title="Pane 3"><p>Lorem</p><p>lorem</p></div>
        <div dojoType="dijit.TitlePane" open="false" title="Pane 4"><p>Lorem</p></div>    
    </div>
    <h2>Content after</h2>

Adding and removing children:


.. code-example::

  .. css::

     <style type="text/css"> 
        @import "{{baseUrl}}dojox/widget/TitleGroup/TitleGroup.css";
     </style>

  .. javascript::

    <script>
        dojo.require("dojox.widget.TitleGroup");
        dojo.require("dijit.TitlePane");
        dojo.require("dijit.form.Button");
    </script>

  .. html::

    <h2>Content before</h2>
    <div data-dojo-type="dijit.form.Button">
       click to add
       <script type="dojo/method" data-dojo-event="onClick">
            var group = dijit.byId("titleGroupB");
            var tp = new dijit.TitlePane({ open:false, title: "Added " + dijit.registry.length });
            group.addChild(tp);
       </script>
    </div>
    <div data-dojo-type="dijit.form.Button">
        pop one off
        <script type="dojo/method" data-dojo-event="onClick">
            dijit.registry.byClass("dijit.TitlePane").some(function(widget){
                  dijit.byId("titleGroupB").removeChild(widget);
                  widget.destroy(); 
                  return true; // only once
            }); 
        </script>
    </div>
    <div id="titleGroupB" style="width:500px" data-dojo-type="dojox.widget.TitleGroup">
        <div dojoType="dijit.TitlePane" open="true" title="Pane 1">
            Pane 1
        </div>
    </div>
    <h2>Content after</h2>
    <div id="graveyard"></div>


See Also:
=========

* `dijit.TitlePane <dijit/TitlePane>`_
* `dijit.layout.AccordionContainer <dijit/layout/AccordionContainer>`_
* `The original blog and motivation <http://www.sitepen.com/blog/2008/10/21/quick-fixes-and-dojo-support/>`_
