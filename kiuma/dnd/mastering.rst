#format dojo_rst

dojo.dnd.Source
===============

:Status: Draft
:Version: 1.0
:Authors: Kiuma
:Developers: ?-
:Available: since V?

.. contents::
    :depth: 2

A Source is a d&d container that may act both like a source and a target for d&d items.

If you have not to do particular requirements, you'll use this class most of the times when you need draggable items, but there are particular cases where you need subclassing and the dojo.dnd package does not always behave as you might expect.

.. code-block :: html
  :linenos:

  <style type="text/css">
     .dndContainer {
        border: 1px solid gray;
        width: 120px;
        padding: 3px;
        height: 200px;
     }
  </style> 
  <script type="text/javascript">
    dojo.require("dojo.dnd.Source");
  </script>
  <div class="dndContainer" dojoType="dojo.dnd.Source">
    <div class="dojoDndItem">item1</div>
    <div class="dojoDndItem">item2</div>
    <div class="dojoDndItem">item3</div>
  </div>


What above is good if you want to reorder items, but is usually not sufficient because I think you want to transfer items from a place to another like, for example a user-role definition. So let's keep with another example.

.. code-block :: html
  :linenos:

  <style type="text/css">
     fieldset.dndContainer {
        border: 1px solid gray;
        width: 120px;
        padding: 3px;
        height: 200px;
        position: relative;
        float: left;
        margin-right: 5px;
     }
  </style>
  <script type="text/javascript">
    dojo.require("dojo.dnd.Source");
  </script>
  <div class="userRoleContainer">
    <fieldset class="dndContainer availableRoles" dojoType="dojo.dnd.Source">
      <legend>Available roles</legend>
      <div class="dojoDndItem">admin</div>
      <div class="dojoDndItem">guest</div>
      <div class="dojoDndItem">publisher</div>
    </fieldset>
    <fieldset class="dndContainer assignedRoles" dojoType="dojo.dnd.Source">
      <legend>Assigned roles</legend>
      <div class="dojoDndItem">user</div>
    </fieldset>
  </div>

This is all good, but suppose that your page has two kind of d&d, a cart-basket and a coupon-basket used to pay via coupon.
So,what you don't want is to put a coupon into the cart-basket and a product into the coupons one, suppose also that the coupon basket accepts card points (yes youo provide a customer with a recharceable card.
So you'll have to mark a Source container with an accept tag attribute (comma separated) to accepts particular items, and you have to mark every draggable item with the appropriate type using dndType tag attribute.

.. code-block :: html
  :linenos:

  <style type="text/css">
     fieldset.dndContainer {
        border: 1px solid gray;
        width: 120px;
        padding: 3px;
        height: 200px;
        position: relative;
        float: left;
        margin-right: 5px;
     }
     .paymentContainer {
       position: relative;
       float: left;
       margin-left: 50px;
     }
  </style> 
  <script type="text/javascript">
    dojo.require("dojo.dnd.Source");
  </script>
  <div class="cartContainer">
    <fieldset class="dndContainer products" dojoType="dojo.dnd.Source" accept="product">
      <legend>Items</legend>
      <div class="dojoDndItem" dndType="product">apple</div>
      <div class="dojoDndItem" dndType="product">pear</div>
      <div class="dojoDndItem" dndType="product">orange</div>
    </fieldset>
    <fieldset class="dndContainer basket" dojoType="dojo.dnd.Source" accept="product">
      <legend>Cart</legend>
    </fieldset>
  </div>
  <div class="paymentContainer">
    <fieldset class="dndContainer couponsAndPoints" dojoType="dojo.dnd.Source" accept="coupon, point">
      <legend>Items</legend>
      <div class="dojoDndItem" dndType="coupon">$ 10.00</div>
      <div class="dojoDndItem" dndType="coupon">$ 5.00</div>
      <div class="dojoDndItem" dndType="point">1 points ($ 1.00)</div>
      <div class="dojoDndItem" dndType="point">2 points ($ 2.00)</div>
    </fieldset>
    <fieldset class="dndContainer basketPoints" dojoType="dojo.dnd.Source" accept="coupon, point">
      <legend>Payment basket</legend>
    </fieldset>
  </div>

Nearly good, ...nearly! 

The cart is not really correct, infact we are moving items, while the correct behaviour should be to copy them to the cart. Also, we don't want a single item to be duplicated inside the cart, but more precisely want so see only how many 'oranges' we have into our basket.

Moreover in a cart you don't want to move items from our stock, you'd prefer to copy them from the items container to the basket/cart, so we'll set the copyOnly property to true for available items.

We also don't want to duplicate items into our basket, but only set how many of the same type we are going to checkout and also we want to remove items one at a time and delete the cart item only when quantity reaches 0.

For this purpose we'll connect to the onDndDrop event.
This event is fired both for the source and the target of the dnd action, so be careful to what they are.

And yes, we need a bit of javascript now!

The example below shows what just explained:

.. code-block :: html
 :linenos:

  <style type="text/css">
     fieldset.dndContainer {
        border: 1px solid gray;
        width: 120px;
        padding: 3px;
        height: 200px;
        position: relative;
        float: left;
        margin-right: 5px;
     }
     .paymentContainer {
       position: relative;
       float: left;
       margin-left: 50px;
     }
  </style> 
  <script type="text/javascript">
    dojo.require("dojo.dnd.Source");
  </script>
  <div class="cartContainer">
    <fieldset id="items" class="dndContainer products" dojoType="dojo.dnd.Source" accept="cartItem" copyOnly="true">
      <script type="dojo/connect" event="onDndDrop" args="source, nodes, copy, target">
          var basket = dojo.byId('basket'); 
          if ((target != source) && (target.node.id == 'items')) {
              dojo.forEach(nodes, function(node){
                var nodeTitle = node.title;
                var basketItemsToRemove = dojo.query('[title=' + nodeTitle + ']', target.node);
                var removeItemSize = basketItemsToRemove.length;
                var basketItem = dojo.query('[title=' + nodeTitle + ']', basket)[0];
                for(var i = removeItemSize-1;i>=0;i--){                 
                  if (dojo.attr(basketItemsToRemove[i], 'quantity') != '0') {
                    basketItemsToRemove[i].parentNode.removeChild(basketItemsToRemove[i]);                    
                    target.delItem(node.id);
                    dojo.attr(basketItem, 'quantity', parseInt(dojo.attr(basketItem, 'quantity')) -1);
                    dojo.forEach(dojo.query('span', basketItem), function(qt) {                   
                      qt.innerHTML = dojo.attr(basketItem, 'quantity');
                    });
                    if (dojo.attr(basketItem, 'quantity') == '0') {
                      basketItem.parentNode.removeChild(basketItem);
                    }
                  }
                }
              });
            
          }
      </script>
      <legend>Stock items</legend>
      <div dndType="cartItem" class="dojoDndItem" title="orange" quantity="0"><span class="quantity"></span> orange</div>
      <div dndType="cartItem" class="dojoDndItem" title="apple" quantity="0"><span class="quantity"></span> apple</div>
      <div dndType="cartItem" class="dojoDndItem" title="pear" quantity="0"><span class="quantity"></span> pear</div>
    </fieldset>
    <fieldset id="basket" class="dndContainer basket" dojoType="dojo.dnd.Source" accept="cartItem" copyOnly="true">
      <script type="dojo/connect" event="onDndDrop" args="source, nodes, copy, target">
          var basket = dojo.byId('basket');  
          if ((target != source) && (target.node.id == 'basket')) { 
              dojo.forEach(nodes, function(node){
                var nodeTitle = node.title;
                var nodeId = node.id;              
                var basketItems = dojo.query('[title=' + nodeTitle + ']', basket);
                
                if ( basketItems.length == 1) {
                  dojo.forEach(dojo.query('.quantity', basketItems[0]), function(qt) {                    
                      qt.innerHTML = 1;                    
                      dojo.attr(basketItems[0], 'quantity', qt.innerHTML);
                  });                    
                } else {                
                  var basketItemsToRemove = dojo.query('[title=' + nodeTitle + ']', basket);
                  var addItemSize = basketItemsToRemove.length;
                  var incSize = 0;
                  var currentItem = null;   
                  for(var i = addItemSize-1;i>=0;i--){                  
                    if (dojo.attr(basketItemsToRemove[i], 'quantity') == '0') {
                      basketItemsToRemove[i].parentNode.removeChild(basketItemsToRemove[i]);
                      incSize++;
                      target.delItem(node.id);
                    } else {
                      currentItem = basketItemsToRemove[i];
                    }
                  }
                   if (currentItem) {
                    dojo.attr(currentItem, 'quantity', parseInt(dojo.attr(currentItem, 'quantity')) + incSize);
                    dojo.forEach(dojo.query('span', currentItem), function(qt) {                    
                       qt.innerHTML = dojo.attr(currentItem, 'quantity');
                    });
                  }                                  
                }            
              });            
          } 
        </script>
      <legend>Cart</legend>
    </fieldset>
  </div>
  <div class="paymentContainer">
    <fieldset class="dndContainer couponsAndPoints" dojoType="dojo.dnd.Source" accept="coupon, point">
      <legend>Cart</legend>
      <div class="dojoDndItem" dndType="coupon">$ 10.00</div>
      <div class="dojoDndItem" dndType="coupon">$ 5.00</div>
      <div class="dojoDndItem" dndType="point">1 points ($ 1.00)</div>
      <div class="dojoDndItem" dndType="point">2 points ($ 2.00)</div>
    </fieldset>
    <fieldset class="dndContainer basketPoints" dojoType="dojo.dnd.Source" accept="coupon, point">
      <legend>Payment basket</legend>
    </fieldset>
  </div>


Now we may want to get back our "dojo.dnd.Source" reference, suppose infact that we are performing an xhr call, and we want to replace the content of an element where there is a dojo.dnd.Source.
For example we might want to use the innerHTML property to replace such content, then we'll need to reparse the element content with the dojo parser. 

.. code-example::
  
  .. javascript::
    :label: Javascript code
    <script type="text/javascript">
      dojo.require('dijit.form.Button');
      dojo.require('dojo.parser');
      dojo.require('dojo.dnd.Source');
      generateRandomContent = function () {
        var strartPoint = Math.floor(Math.random()*10);
        var htmlContent = "<div dojotype='dijit.form.Button' onclick='sample.updateNumberDragging()'>Generate random content</div>\n";
        htmlContent += "<fieldset class='dndContainer numbers' dojoType='dojo.dnd.Source' accept='number'>\n"; 
        htmlContent += "<script type='dojo/connect' event='onDndDrop' args='source, nodes, copy, target'>\nconsole.debug('dropping ' + nodes[0].innerHTML + '...');\n</script>\n"; 
        htmlContent += "<legend>Numbers</legend>\n"; 
        for (var i = strartPoint; i < strartPoint + 10; i++) {
          htmlContent += "<div class='dojoDndItem' dndType='number'>"+i+"</div>\n"; 
        } 
        htmlContent += "</fieldset></div>\n"; 
        var numberDragging = dojo.byId('numberDragging');
        dojo.forEach(
          dojo.query(['widgetid']).map(dijit.byNode),
          function (widget) {
            if (widget) {widget.destroy();}
          });
        numberDragging.innerHTML = htmlContent;
        dojo.parser.parse(numberDragging);
        dojo.connect(dojo.byId('buttonGenerator'),
                   'onclick',
                   generateRandomContent);
      };
      dojo.addOnLoad(function () {
        alert(1);
        dojo.connect(dojo.byId('buttonGenerator'),
                   'onclick',
                   generateRandomContent);
      }
    </script>

  .. html::
    :label: Dragging html

    <div id="numberDragging">
      <div id="buttonGenerator" dojotype='dijit.form.Button'>Generate random content</div>
      <fieldset class='dndContainer numbers' dojoType='dojo.dnd.Source' accept='number'>
        <script type="dojo/connect" event="onDndDrop" args="source, nodes, copy, target">
          console.debug("dropping " + nodes[0].innerHTML + "...");
        </script>
        <legend>Numbers</legend>
        <div class="dojoDndItem" dndType="number">1</div>
        <div class="dojoDndItem" dndType="number">2</div>
        <div class="dojoDndItem" dndType="number">3</div>
        <div class="dojoDndItem" dndType="number">4</div>
        <div class="dojoDndItem" dndType="number">5</div>
        <div class="dojoDndItem" dndType="number">6</div>
        <div class="dojoDndItem" dndType="number">7</div>
        <div class="dojoDndItem" dndType="number">8</div>
        <div class="dojoDndItem" dndType="number">9</div>
        <div class="dojoDndItem" dndType="number">10</div>
      </fieldset>
    </div>


We can then use the special data-dojo-id tag attribute, that allows us to map a global variable provided by data-dojo-id over our dojo.dnd.Source. See `data-dojo-id, dijit.byId() and dojo.byId() <dijit/byId#data-dojo-id-dijit-byid-and-dojo-byid>`_ for more info.

Finished? ...not yet!

dojo.dnd.Source and its parents dojo.dnd.Selector and dojo.dnd.Container are a little strange classes.

First, once attacched to a tag element via dojotype tag attribute, you are not able to get the dojo.dndSource instance anymore, it will be 'lost'
inside the window.document.

In addiction the initialize (and the destroy too) method doesn't behave like you might expect as described here `dojo.dnd subclassing <dojo/dnd#subclassing-dnd-classes>`_

.. code-example::
  
  .. javascript::

    <script type="text/javascript">
      dojo.require("dijit.form.Button");
    </script>

  .. html::

    <div id="numberDragging2">      
      <div onclick="alert(sample);">show sample</div> 
      <div dojoType="dijit.form.Button" onclick="sample.updateNumberDragging()">Generate random content</div>
    </div>

Ok, we are finished...
