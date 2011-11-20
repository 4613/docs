#format dojo_rst

Dojox
=====

DojoX serves many purposes, and by design is difficult to document. Here, we have an ongoing effort to document the most used, stable, reliable and powerful aspects of DojoX. DojoX contains code in alpha and experimental states, so your assistance in testing and documenting are especially helpful.

These sections cover the available projects shipped with the Dojo Toolkit

* `Information <dojox/info>`_

* `dojox <dojox>`_
* `dojox.analytics <dojox/analytics>`_

  * `dojox.analytics.Urchin <dojox/analytics/Urchin>`_

* `dojox.av <dojox/av>`_
* `dojox.charting <dojox/charting>`_

  Amazing charting library

* `dojox.collections <dojox/collections>`_
* `dojox.color <dojox/color>`_
* `dojox.cometd <dojox/cometd>`_
* `dojox.data <dojox/data>`_

  Additional data stores and data store helpers

  * `dojox.data.AndOrReadStore <dojox/data/AndOrReadStore>`_

    A clone of `dojo.data.ItemFileReadStore <dojo/data/ItemFileReadStore>`__, which supports more complex queries than the simple AND format property matching

  * `dojox.data.AndOrWriteStore <dojox/data/AndOrWriteStore>`_

    A clone of `dojo.data.ItemFileWriteStore <dojo/data/ItemFileWriteStore>`__, which supports more complex queries than the simple AND format property matching

  * `dojox.data.AtomReadStore <dojox/data/AtomReadStore>`_

    A store designed to provide read-only access to Atom XML documents

  * `dojox.data.ClientFilter <dojox/data/ClientFilter>`_

    An abstract data store module for adding updateable result set functionality to an existing data store class

  * `dojox.data.CouchDBRestStore <dojox/data/CouchDBRestStore>`_

    An extension of `dojox.data.JsonRestStore <dojox/data/JsonRestStore>`_ to handle CouchDB's idiosyncrasies, special features, and deviations from standard HTTP Rest

  * `dojox.data.CssClassStore <dojox/data/CssClassStore>`_

    A read interface based on the `dojox.data.CssRuleStore <dojox/data/CssRuleStore>`_

  * `dojox.data.CssRuleStore <dojox/data/CssRuleStore>`_

    A read interface to the CSS rules loaded in the current page

  * `dojox.data.CsvStore <dojox/data/CsvStore>`_

    A read interface that works with CSV formated data files

  * `dojox.data.FileStore <dojox/data/FileStore>`_

    A lightweight data store implementation for accessing details about a remote FileSystem

  * `dojox.data.FlickrRestStore <dojox/data/FlickrRestStore>`_

    Provides access to the Flickr photo sharing site's REST API

  * `dojox.data.FlickrStore <dojox/data/FlickrStore>`_

    A wrapper to the public photo feed of the Flickr service

  * `dojox.data.GoogleFeedStore <dojox/data/GoogleFeedStore>`_

    A Google AJAX API powered data store for retrieving RSS and Atom feeds from Google

  * `dojox.data.GoogleSearchStore <dojox/data/GoogleSearchStore>`_

    Several data stores to interface Google's AJAX search services:

    * `dojox.data.GoogleWebSearchStore <dojox/data/GoogleWebSearchStore>`_

      A data store for retrieving search results from Google

    * `dojox.data.GoogleBlogSearchStore <dojox/data/GoogleBlogSearchStore>`_

      A data store for retrieving search results from Google Blogs

    * `dojox.data.GoogleLocalSearchStore <dojox/data/GoogleLocalSearchStore>`_

      A data store for retrieving search results from Google Location Search

    * `dojox.data.GoogleVideoSearchStore <dojox/data/GoogleVideoSearchStore>`_

      A data store for retrieving search results from Google Video

    * `dojox.data.GoogleNewsSearchStore <dojox/data/GoogleNewsSearchStore>`_

      A data store for retrieving search results from Google News

    * `dojox.data.GoogleBookSearchStore <dojox/data/GoogleBookSearchStore>`_

      A data store for retrieving search results from Google Book

    * `dojox.data.GoogleImageSearchStore <dojox/data/GoogleImageSearchStore>`_

      A data store for retrieving search results from Google Image

  * `dojox.data.HtmlStore <dojox/data/HtmlStore>`_

    An enhanced replacement for `dojox.data.HtmlTableStore <dojox/data/HtmlTableStore>`_ to work with HTML tables, lists, and collections of DIV and SPAN tags.

  * `dojox.data.HtmlTableStore <dojox/data/HtmlTableStore>`_ (*deprecated*)

    A read interface to work with HTML tables

  * `dojox.data.jsonPathStore <dojox/data/jsonPathStore>`_

    A local (in memory) store which can attach a dojo.data interface to each javascript object and uses jsonPath as the query language

  * `dojox.data.JsonRestStore <dojox/data/JsonRestStore>`_

    A lightweight data store implementation of a RESTful client

  * `dojox.data.KeyValueStore <dojox/data/KeyValueStore>`_

    An interface for reading property style files (key/value pairs)

  * `dojox.data.OpmlStore <dojox/data/OpmlStore>`_

    A read-only store to work with Opml formatted XML files

  * `dojox.data.PersevereStore <dojox/data/PersevereStore>`_

    An extension of `dojox.data.JsonRestStore <dojox/data/JsonRestStore>`_ to handle Persevere's special features

  * `dojox.data.PicasaStore <dojox/data/PicasaStore>`_

    A data store interface to one of the basic services of the Picasa service, the public photo feed

  * `dojox.data.QueryReadStore <dojox/data/QueryReadStore>`_

    A read-only store, which makes a request to the server for each sorting or query in order to work with big datasets

  * `dojox.data.S3Store <dojox/data/S3Store>`_

    An extension of `dojox.data.JsonRestStore <dojox/data/JsonRestStore>`_ to handle Amazon's S3 service using JSON data

  * `dojox.data.ServiceStore <dojox/data/ServiceStore>`_

    ServiceStore and it's subclasses are a generalized dojo.data implementation for any webservice

  * `dojox.data.SnapLogicStore <dojox/data/SnapLogicStore>`_

    A data store interface to use the SnapLogic framework

  * `dojox.data.WikipediaStore <dojox/data/WikipediaStore>`_

    An extension of `dojox.data.ServiceStore <dojox/data/ServiceStore>`_ to use Wikipedia's search service

  * `dojox.data.XmlStore <dojox/data/XmlStore>`_

    A read and write interface to basic XML data

* `dojox.date <dojox/date>`_
* `dojox.dtl <dojox/dtl>`_
* `dojox.editor <dojox/editor>`_
* `dojox.embed <dojox/embed>`_
* `dojox.encoding <dojox/encoding>`_
* `dojox.flash <dojox/flash>`_
* `dojox.form <dojox/form>`_

  Additional form-related widgets beyond `dijit.form <dijit/form>`_ functionality

  * `dojox.form.BusyButton <dojox/form/BusyButton>`_

    A new Button with progresss indicator built in, for indicating processing after you press the button

  * dojox.form.CheckedMultiSelect

    description?

  * dojox.form.DateTextBox

    description?

  * dojox.form.DropDownSelect

    description?

  * dojox.form.DropDownStack

    description?

  * dojox.form.FileInput (base, Auto, and Blind)

    description?

  * `dojox.form.FilePickerTextBox <dojox/form/FilePickerTextBox>`_

    A dijit._FormWidget that adds a dojox.widget.FilePicker to a text box as a dropdown

  * `dojox.form.FileUploader <dojox/form/FileUploader>`_

    A new multi-file uploader that shows progress as the files are uploading

  * `dojox.form.manager (the package) <dojox/form/manager>`_

    A collection of mixins to manage complex event-driven dynamic forms

    * `dojox.form.Manager (the widget) <dojox/form/Manager>`_

      A simple widget based on `dojox.form.manager <dojox/form/manager>`_ package.

  * dojox.form.MultiComboBox

    description?

  * dojox.form.PasswordValidator

    description?

  * dojox.form.RadioStack

    description?

  * dojox.form.RangeSliders

    description?

  * dojox.form.Rating

    description?

  * dojox.form.TimeSpinner

    description?


* `dojox.fx <dojox/fx>`_

  * `dojox.fx.wipeTo <dojox/fx/wipeTo>`_

* `dojox.gfx <dojox/gfx>`_
* `dojox.gfx3d <dojox/gfx3d>`_
* `dojox.grid <dojox/grid>`_

  A visual grid/table much like a spreadsheet

* `dojox.help <dojox/help>`_
* `dojox.highlight <dojox/highlight>`_
* `dojox.html <dojox/html>`_

  Additional HTML helper functions

  * `dojox.html.set <dojox/html/set>`_

    A generic content setter, including adding new stylesheets and evaluating scripts (was part of ContentPane loaders, now separated for generic usage)

  * `dojox.html.metrics <dojox/html/metrics>`_

    Translate CSS values to pixel values, calculate scrollbar sizes and font resizes

  * `dojox.html.styles <dojox/html/styles>`_

    Insert, remove and toggle CSS rules as well as search document for style sheets

* `dojox.image <dojox/image>`_

  Provides a number of image-related widgets

  * `dojox.image.Badge <dojox/image/Badge>`_

    Attach images or background images, and let them loop

  * `dojox.image.FlickrBadge <dojox/image/FlickrBadge>`_

    An extension on dojox.image.Badge, using Flickr as a data provider

  * `dojox.image.Gallery <dojox/image/Gallery>`_

    A combination of a SlideShow and ThumbnailPicker

  * `dojox.image.Lightbox <dojox/image/Lightbox>`_

    A widget which shows a single image (or groups of images) in a Dialog

  * `dojox.image.Magnifier <dojox/image/Magnifier>`_

    A dojox.gfx-based version of the `MagnifierLite <dojox/image/MagnifierLite>`_ widget

  * `dojox.image.MagnifierLite <dojox/image/MagnifierLite>`_

    A simple hover behavior for images, showing a zoomed version of a size image

  * `dojox.image.SlideShow <dojox/image/SlideShow>`_

    A slideshow of images

  * `dojox.image.ThumbnailPicker <dojox/image/ThumbnailPicker>`_

    A dojo.data-powered ThumbnailPicker

* `dojox.io <dojox/io>`_
* `dojox.json <dojox/json>`_
* `dojox.jsonPath <dojox/jsonPath>`_
* `dojox.lang <dojox/lang>`_
* `dojox.layout <dojox/layout>`_

  Experimental and additional extensions to `Dijit Layout <dijit/layout>`__ Widgets

  * `dojox.layout.ContentPane <dojox/layout/ContentPane>`_

    An extension to dijit.layout.ContentPane providing script execution, among other things

  * `dojox.layout.DragPane <dojox/layout/DragPane>`_

    Provides drag-based scrolling for divs with overflow

  * `dojox.layout.ExpandoPane <dojox/layout/ExpandoPane>`_

    A self-collapsing widget for use in a `BorderContainer <dijit/layout/BorderContainer>`__

  * `dojox.layout.FloatingPane <dojox/layout/FloatingPane>`_

    An experimental floating window

  * `dojox.layout.GridContainer <dojox/layout/GridContainer>`_

    A panel-like layout mechanism, allowing Drag and Drop between regions

  * `dojox.layout.RadioGroup <dojox/layout/RadioGroup>`_

    A variety of `StackContainer <dijit/layout/StackContainer>`__ enhancements providing animated transitions

  * `dojox.layout.ResizeHandle <dojox/layout/ResizeHandle>`_

    A small widget to provide resizing of a parent node

  * `dojox.layout.RotatorContainer <dojox/layout/RotatorContainer>`_

    An extended StackContainer suited for presentational purposes

  * `dojox.layout.ScrollPane <dojox/layout/ScrollPane>`_

    An interesting UI, scrolling an overflowed div based on mouse position, either vertical or horizontal

  * `dojox.layout.ToggleSplitter <dojox/layout/ToggleSplitter>`_

    A custom Splitter for use in a BorderContainer, providing a lightweight way to collapse the associated child

* `dojox.math <dojox/math>`_
* `dojox.off <dojox/off>`_
* `dojox.presentation <dojox/presentation>`_
* `dojox.resources <dojox/resources>`_
* `dojox.robot <dojox/robot>`_
* `dojox.rpc <dojox/rpc>`_

  Extended classes to communicate via Remote Procedure Calls (RPC) with Backend Servers

  * `dojox.rpc.SMDLibrary <dojox/rpc/SMDLibrary>`_
  * `dojox.rpc.Client <dojox/rpc/Client>`_
  * `dojox.rpc.JsonRest <dojox/rpc/JsonRest>`_
  * `dojox.rpc.JsonRPC <dojox/rpc/JsonRPC>`_
  * `dojox.rpc.LocalStorageRest <dojox/rpc/LocalStorageRest>`_
  * `dojox.rpc.OfflineRest <dojox/rpc/OfflineRest>`_
  * `dojox.rpc.ProxiedPath <dojox/rpc/ProxiedPath>`_
  * `dojox.rpc.Rest <dojox/rpc/Rest>`_
  * `dojox.rpc.Service <dojox/rpc/Service>`_

* `dojox.secure <dojox/secure>`_
* `dojox.sql <dojox/sql>`_
* `dojox.storage <dojox/storage>`_
* `dojox.string <dojox/string>`_
* `dojox.testing <dojox/testing>`_
* `dojox.timing <dojox/timing>`_
* `dojox.uuid <dojox/uuid>`_
* `dojox.validate <dojox/validate>`_
* `dojox.widget <dojox/widget>`_

  * `dojox.widget.AnalogGauge <dojox/widget/AnalogGauge>`_

    A circular gauge with a variety of indicators, used to display numerical data

  * `dojox.widget.BarGauge <dojox/widget/BarGauge>`_

    A horizontal bar gauge with a few indicators, used to display numerical data

  * `dojox.widget.Calendar <dojox/widget/Calendar>`_

    An extended dijit._Calendar

  * `dojox.widget.CalendarFx <dojox/widget/CalendarFx>`_

    An extended dijit._Calendar with FX

  * `dojox.widget.ColorPicker <dojox/widget/ColorPicker>`_

    A HSV Color Picker, similar to PhotoShop

  * `dojox.widget.Dialog <dojox/widget/Dialog>`_

    An extension to `dijit.Dialog </dijit/Dialog>`__ which provides additional sizing options, animations, and styling

  * `dojox.widget.DocTester <dojox/widget/DocTester>`_

    A widget to run DocTests inside an HTML page

  * `dojox.widget.FilePicker <dojox/widget/FilePicker>`_

    A specialized version of RollingList that handles file informatione

  * `dojox.widget.FisheyeList <dojox/widget/FisheyeList>`_

    A OSX-style Fisheye Menu

  * `dojox.widget.FisheyeLite <dojox/widget/FisheyeLite>`_

    A more robust Fisheye Widget, which fish-eyes' any CSS property

  * `dojox.widget.Iterator <dojox/widget/Iterator>`_

    A basic array and data store iterator class

  * `dojox.widget.Loader <dojox/widget/Loader>`_

    A small experimental Ajax Activity indicator (deprecated, will be moved to dojo-c)

  * `dojox.widget.Pager <dojox/widget/Pager>`_

    A `dojo.data <dojo/data>`_ powered Pager Widget, displaying a few items in a horizontal or vertical UI

  * `dojox.widget.PlaceholderMenuItem <dojox/widget/PlaceholderMenuItem>`_

    A menu item that can be used as a placeholder.

  * `dojox.widget.Roller <dojox/widget/Roller>`_

    An unobtrusive "roller", displaying one message from a list in a loop

  * `dojox.widget.RollingList <dojox/widget/RollingList>`_

    A rolling list that can be tied to a data store with children

  * `dojox.widget.SortList <dojox/widget/SortList>`_

    A small sortable unordered-list

  * `dojox.widget.Standby <dojox/widget/Standby>`_

    A small widget that can be used to mark sections of a page as busy, processing, unavailable, etc.

  * `dojox.widget.Toaster <dojox/widget/Toaster>`_

    A message display system, showing warnings, errors and other messages unobtrusively

  * `dojox.widget.Wizard <dojox/widget/Wizard>`_

    A simple widget providing a step-by-step wizard like UI

* `dojox.wire <dojox/wire>`_
* `dojox.xml <dojox/xml>`_
* `dojox.xmpp <dojox/xmpp>`_
