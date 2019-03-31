---
title: dijit.Dialog in Domino XPages
date: "2009-04-16"
template: "post"
draft: false
slug: "/posts/2009/dijit-dialog-domino-xpages/"

tags:
- "old"
- "xpages"
- "domino"
- "dijit"
- "dojo"
description: "# Background"
---
# Background

When dojo (what XPages basically runs off) creates a dijit.Dialog, it moves the dialog DOM node to the root document <body> node to ensure that the dialog is rendered above all other elements.

# The Problem

I have an XPage in which I want to display two fields in one location, in this case it is a companies name as well as their trading name.  I wanted to create a dojo form for entering the two fields and display the two fields in one place (Company A trading as Trading Name).  I thought using the dijit.Dialog that comes with dojo would be a perfect fit, hoping it would work out of the box.

Like all other IBM solutions, that was not to be the case.

This is how I started.

	<xp:panel id="name">
	  <h1>
		<xp:text id="edtName">
		<xp:this.value><![CDATA[#{javascript:
	var ret = document.getItemValueString('provCoName');
	var a = document.getItemValueString('provTradName');
	if(a!=null&&a!=''&&a!='null'){ret+=' trading as '+a;}
	return ret;}]]></xp:this.value>
		</xp:text>
	  </h1>
	</xp:panel>
	<xp:panel rendered="#{javascript:return document.isEditable();}">
	  <button dojoType="dijit.form.Button">Edit 
	  <script type="dojo/method" event="onClick" args="evt">
	  dijit.byId("name_dialog").show();</script></button>
	  <div id="name_dialog" dojoType="dijit.Dialog"
	  title="Company Name">
		<table style="width:100%">
		  <tr>
			<td>Company Name:</td>
			<td>
			  <xp:inputText value="#{document.provCoName}" />
			</td>
		  </tr>
		  <tr>
			<td>Trading Name:</td>
			<td>
			  <xp:inputText value="#{document.provTradName}" />
			</td>
		  </tr>
		  <tr>
			<td colspan="2" style="text-align:right">
			  <xp:button value="Save" id="btnNameSave">
				<xp:eventHandler event="onclick" submit="true"
				refreshMode="partial" refreshId="name">
				  <xp:this.handlers>
					<xp:handler type="text/javascript">
					  <xp:this.script>
						<![CDATA[var d = dijit.byId('name_dialog');
	d.hide();
	return true;]]>
	</xp:this.script>
					</xp:handler>
				  </xp:this.handlers>
				</xp:eventHandler>
			  </xp:button>
			</td>
		  </tr>
		</table>
	  </div>
	</xp:panel>

It's all fairly straight forward, a dialog is created with the two XPages fields in it and a button to submit the changes to Domino and do a partial update of the name section to be updated when new data has been entered, a button is also created to display the dialog.

The problem with what I have above is that, as mentioned in the background above, dojo moves the dialog's HTML DOM node to the document body node, which happens to fall outside the XPages-generated form node, rendering all fields and controls inside the dialog useless, to XPages anyway.

After reading around and consulting some dojo experts I came to the conclusion that some client-side scripting would be required to move the dialog's DOM node from the document body to the form's node.  As the form node takes up the entirity of the body node this should not cause any issues.

Here is the code I used to achieve this.

	dojo.addOnLoad(xx_init);

	function xx_init()
	{
		move_dialogs();
	}

	function move_dialogs()
	{
		var form = document.forms[0];
		var list = dojo.query('.dijitDialog');
		
		for (var i = 0; i < list.length; i++)
		{
			var e = list[i];

			form.appendChild(e);
		}
	}

# Conclusion

After moving the dialogs to the form node, the page worked perfectly and as expected.