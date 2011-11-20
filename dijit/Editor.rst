## page was renamed from 1.2/dijit/Editor
## page was renamed from dijit/Editor
#format dojo_rst

dijit.Editor
============

:Status: Draft
:Version: 1.2

Dijit's Rich Text editor, Dijit.Editor, is a text box on steroids. Designed to look and work like a word processor. The editor features a toolbar, HTML output, and a plugin architecture that supports new commands, new buttons and other new features.


.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
      dojo.require("dijit.Editor");
    </script>

  .. cv:: html

      <div dojoType="dijit.Editor" id="editor1" onChange="console.log('editor1 onChange handler: ' + arguments[0])">
        <p>This instance is created from a div directly with default toolbar and plugins</p>
      </div>


Plugins
-------

A plugin (a.k.a. extension) is something that adds a function to the editor, or changes it's behavior.
Dojo includes a number of editor plugins, and developers can write additional plugins on their own.

Most plugins have an associated toolbar button(s), such as the FontChoice plugin (which has a drop down list for fonts),
but some plugins (like AlwaysShowToolbar) just affect the Editor's behavior without changing the toolbar.

The "plugins" parameter controls which plugins are available, and also controls which builtin editor commands
are available.

If you want to just add plugins above and beyond the standard configuration, then you should use the "extraPlugins" parameter.

Both the "plugins" parameter and the "extraPlugins" parameter are arrays, where each element in the array can be a
simple string or an object (if you need to set options on a plugin).

This example adds the text color, background color, and font selection plugins to the editor by setting extraPlugins.
(Technically, the FontChoice plugin provides two commands, foreground-color and highlight-color.)

.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
      dojo.require("dijit.Editor");
      dojo.require("dijit._editor.plugins.FontChoice");  // 'fontName','fontSize','formatBlock'
      dojo.require("dijit._editor.plugins.TextColor");
    </script>

  .. cv:: html

      <div dojoType="dijit.Editor" id="editor2"
	extraPlugins="['foreColor','hiliteColor',{name:'dijit._editor.plugins.FontChoice', command:'fontName', generic:true}]"
        onChange="console.log('editor2 onChange handler: ' + arguments[0])">
        <p>This instance is created with additional toolbar/ plugins</p>
      </div>

This example starts from scratch, thus removing some items from the toolbar (as compared to the default), like underline, and adding other features, namely the LinkDialog:

.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
      dojo.require("dijit.Editor");
      dojo.require("dijit._editor.plugins.LinkDialog");
    </script>

  .. cv:: html

      <div dojoType="dijit.Editor" id="editor3"
	plugins="['bold','italic','|','createLink']"
        onChange="console.log('editor3 onChange handler: ' + arguments[0])">
        <p>This instance is created with customized toolbar/ plugins</p>
      </div>


This is a list of the default commands included in the editor, that can be specified in the plugins parameter (in addition to actual editor plugins in the editor/plugins directory or other places):

* "undo"
* "redo"
* "cut"
* "copy"
* "paste"
* "selectAll"
* "bold"
* "italic"
* "underline"
* "strikethrough"
* "subscript"
* "superscript"
* "removeFormat"
* "insertOrderedList"
* "insertUnorderedList"
* "insertHorizontalRule"
* "indent"
* "outdent"
* "justifyLeft"
* "justifyRight"
* "justifyCenter"
* "justifyFull"
* "createLink"
* "unlink"
* "delete" 

Auto-expanding editor
---------------------
Typically an editor has a constant height, and if there's a lot of content it gets a scrollbar.
This is in addition to the main scrollbar for the page.

Editor also has a mode like dijit.form.Textarea where the more a user types, the more the text box expands.

However, that's a bit tricky because if implemented naively the toolbar would eventually scroll off the top
of the page.

The AlwaysShowToolbar plugin prevents that.  It's used along with setting height="" parameter setting.


.. cv-compound::

  .. cv:: javascript

    <script type="text/javascript">
      dojo.require("dijit.Editor");
      dojo.require("dijit._editor.plugins.AlwaysShowToolbar");
    </script>

  .. cv:: html

        <div dojoType="dijit.Editor" id="editor5"
	   extraPlugins="['dijit._editor.plugins.AlwaysShowToolbar']">
			<p>
				This editor is created from a div with AlwaysShowToolbar plugin (do not forget to set height="").
			</p>
	</div>

Programmatic Creation
---------------------
Of course, the editor can be created programmatically in addition to declaratively,
although even when created programatically you need to specify a source DOM node to replace:

.. cv:: html

	<div id="programmatic2">This div will become an auto-expanding editor.</div>
	<button
		id="create2"
		onclick="new dijit.Editor({height: '', extraPlugins: ['dijit._editor.plugins.AlwaysShowToolbar']}, dojo.byId('programmatic2')); dojo.query('#create2').orphan();">
	create expanding editor
	</button>
