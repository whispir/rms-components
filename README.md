Whispir - Rich Message Studio
==============

The Rich Message Studio is an intuitive interface which used to create rich messages. The content of these rich messages can be built using a library of template components, previewed as they would appear on a mobile device, saved, versioned, and finally sent. 

This repository contains a library of customised components developed by the Whispir Team that can easily be imported into the Rich Message Studio within the Whispir Platform.

# Components

## About Components

**Components** are extensible 'snippits' of content that form the basic building blocks of rich messages. Any number of components can be assembed to create rich messages and interactive mini-applications, which are then served by the Whispir platform.

Components can be extended and built from the ground up to allow template builders and developers the facility to create any component they can imagine.

Components are defined using languages and tools developers use today, namely **HTML**, **Javascript**, and **JSON** - making it simple to build new ones, and easy to re-use existing assets.

## Using components

Whispir provides a number of default Components out of the box. These components help facilitate basic authoring, and act as a starting point to build your own components.

* Components can used by **dragging and dropping** them from the component library onto the composition area.
* Any Component on the composition area can then be modified by hovering, and clicking the **Edit** action. 
* Editing a Component will display the **Properties** of this component within the right sidebar. For example, an image component will have properties to select the image to be displayed, and perhaps properties to modify it's height and width. 

## Structure of a Component

Components are structured in the following way;

1. The basic building block of a Component is '**Markup**', which can be any type of displayable content such as Plain Text or Rich HTML. When used in Rich Messages, Markup can also contain inline **CSS** and **Javascript** to build interactive components.

2. Each Markup building block can optionally include one or more '**Element**'(s). An '**Element**' defines any references used in the Markup, such as a paragraph of HTML, an Image, a File, or a textual field. 

3. Each '**Element**' must contain one or more '**Properties**' that define name/value pairs of data to drive the 'Element', ie; (an Image URL, or Image description)

The following sample structure illustrates this relationship;

- Markup (HTML)
	- Element (Image)
		- Property (URI)
		- Property (Height)
	- Element (Paragraph)
		- Property (RichText)

## Customising a Component

Components provide devolopers a **build once, re-use many** approach to building templates and HTML5 apps.
 
### By Example

Markup source and Properties of a Component can be accessed through the **Code** tab when editing a component.

Components *may* be built with only Markup. Entering this HTML code in the **Markup** tab will then render the result within the Component.

	<h1>Hello World</h1>
	<p>It's a wonderful day</p>

However, editing **Markup** directly makes it difficult for anyone other than a developer to modify this component. 

This is where **Elements** come in. We can define an Element  of "RichText" type in the component, which will then display a text editor in the left sidebar allowing anyone to edit the text. 

Enter the following JSON code in the **Properties** tab;

	[
	    {
	        "element": {
	            "name": "Hello World Paragraph",
	            "reference": "paragraph",
	            "properties": [
	                {
	                    "property": {
	                        "type": "RichText",
	                        "name": "Hello World Paragraph",
	                        "value": "Hi right back, <b>World</b>!",
	                        "reference": "mytext"
	                    }
	                }
	            ]
	        }
	    }
	]
	
The **Markup** is now updated to reference the Element;

	<h1>Hello World</h1>
	<p>[[paragraph.mytext]]</p>

Now, when editing this component a text editor will appear, and allow anyone to easily update the paragraph of text.

## Editing Component code

##### Markup 

Can include any valid HTML, inline Javascript or inline CSS.

	 <div class="myDiv">
	     <img class="myImg" src="[[photo.src]]"/>
	     <p>[[paragraph.mytext]]</p>
	 <div>
	 
	 <style>
	   .myImg { width: [[photo.width]]; }
	   .myDiv { text-align: center; margin: 10px;}
	 </style>
		
##### Properties

JSON array of Element object(s)

	[
	    {
	        "element": {
	            "name": "Profile Photo",
	            "reference": "photo",
	            "properties": [
	                {
	                    "property": {
	                        "type": "Image",
	                        "name": "Profile Photo",
	                        "value": "",
	                        "reference": "src"
	                    }
	                },
	                {
	                    "property": {
	                        "type": "Text",
	                        "name": "Width (in %)",
	                        "value": "50%",
	                        "reference": "width"
	                    }
	                }
	            ]
	        }
	    },
	    {
	        "element": {
	            "name": "Profile Description",
	            "reference": "paragraph",
	            "properties": [
	                {
	                    "property": {
	                        "type": "RichText",
	                        "name": "Profile Details",
	                        "value": "My <b>details</b>",
	                        "reference": "mytext"
	                    }
	                }
	            ]
	        }
	    }	    
	]
	
##### Scripts

JSON array of Javascript resource URLs.

	[
	    "http://content.whispir.com/public/template/lib/plugins/v1.6.js",
	    "https://maps.googleapis.com/maps/api/js"
	]

* These are external javascript resources which are loaded in the <head> of a Rich Message. 

## Defining Properties

### How properties work

Properties provide an easy way for developers to expose features of their components within the sidebar. 

These features might include;

* A body of **text** which can be edited and formatted in an editor.
* An **image** to be displayed, including it's height and width.  
* A **link** to a video.
* A **location** to be displayed on a map.

For example, you may have just developed a component that displays an image with a caption. Instead of replacing the image manually in the HTML or editing the text inline, you can expose these as **Image** and **Text** property types in your Markup.

Now, when someone uses your component, they can browse in an image, or edit the text caption without editing the HTML directly.

### Property types

Proterties are defined using four primary types;


| Type        | Displays in the sidebar                                        | Accepts                      |
|-------------|----------------------------------------------------------------|------------------------------|
| *Text*      | Small plain text input field                                   | Any text string              |
| *PlainText* | Large Plain text editor                                        | Body of plain text           |
| *RichText*  | Rich HTML text editor                                          | Rich text, basic HTML markup |
| *Image*     | Widget to upload an image, or select from the resource library | Any image resource           |
| *Resource*  | Widget to upload a file, such as a CSS or PDF file             | Any text / binary file       |
| *DropList*  | An dropdown list which provides one or more options to select  | Array of Strings             |

### Property Samples

The following is an sample of all Properties used within a "Customer Profile" Element;

	[
	    {
	        "element": {
	            "name": "Customer Profile",
	            "reference": "customerprofile",
	            "properties": [
	                {
	                    "property": {
	                        "name": "Customer Name",
	                        "value": "Jack Citizen",
	                        "type": "Text",
	                        "reference": "name"
	                    }
	                },
	                {
	                    "property": {
	                        "name": "Customer Photo",
	                        "value": "",
	                        "type": "Image",
	                        "reference": "photo"
	                    }
	                },	                
	                {
	                    "property": {
	                        "name": "Customer Type",
	                        "value": "VIP",
	                        "type": "Droplist",
	                        "options": ["VIP","Regular"],
	                        "reference": "type"
	                    }
	                },
	                {
	                    "property": {
	                        "name": "Customer Description",
	                        "value": "A VIP Customer who is always welcoming",
	                        "type": "PlainText",
	                        "reference": "description"
	                    }
	                },
	                {
	                    "property": {
	                        "name": "Customer Invoice",
	                        "value": "",
	                        "type": "Resource",
	                        "reference": "invoice"
	                    }
	                },
	                {
	                    "property": {
	                        "name": "Message to Customer",
	                        "value": "<p><b>Details</b></p><p>Invoice details</p>",
	                        "type": "RichText",
	                        "reference": "msg"
	                    }
	                }
	            ]
	        }
	    }
	]

#### Referencing properties

Properties can be referenced within any content placed in the **Markup** tab, as follows;

		[[element_name.property_reference]]

Using the previous "Customer Profile" example above;
	
	<div class="customerinvoice">
		<h1>Your Invoice</h1>
		<p>
			<img src="[[customerprofile.photo]]">
		</p>
		<p>
			Hi <strong>[[customerprofile.name]]</strong>
		</p>
		<p>
			[[customerprofile.msg]]
		</p>
		<p>
			{{#if-cond '[[customerprofile.type]]' '==' 'VIP'}}
			Thanks for your continued loyalty!
			{{/if-cond}}
		</p>
		<p>
			<a href="[[customerprofile.invoice]]">Access Your Invoice</a>
		</p>
	</div>
		
	<style>
		.customerinvoice {
			color: #888;
			margin: 20px;
			font-family: sans-serif;
			}
		img {
			width: 100%;			}
	</style>



### Using Component IDs to provide uniqueness

All components within a template have a unique id which is generated at runtime. This ID provides a unique identifier, and allows the same component to be used more than once within the same template.

This is useful if your Markup references CSS styles, HTML elements, or Javascript variables which require a local scope.

The ID can be included within the Markup using the [[id]] value, as follows;

	<img id="photo_[[id]]" src="[[photo.src]]"/>
	
	<style>
		#photo_[[id]] { width: [[photo.width]] }
	</style>
		
	<script>
		var myPhoto[[id]] = document.getElementById("photo_[[id]]");
	</script>
	
This will be rendered at runtime as;

	<img id="photo_654321" src="foobar.jpg"/>
	
	<style>
		#photo_654321 { width: 50% }
	</style>
		
	<script>
		var myPhoto654321 = document.getElementById("photo_654321");
	</script>


## Map Example

	<div class="map">
		<p>How to get to 
		<span id="address-[[id]]">[[loc.address]]</span>
		</p>
		<div id="map-container-[[id]]"></div>
	</div>

	<style>
	 .map {
	    margin: 0 auto;
	    padding: 8px;
	    text-align: center;
	 }
	 #map-container-[[id]] {
	    text-align: center;
	    margin: 0 auto;
	    background-color: #eee;
	    width: 100%;
	    height: 200px;
	    left: 0;
	    top: 0;
	    display: block;
	    border: 1px solid #ccc;
	    max-width: 600px;
	   }
	</style>

	<script>
		// Show Map based on an address
		// ---------

		Whispir.plugins.showMap.init({ 
			address: '111 Exhibition Street, Melbourne, VIC', 
			// Default address used if none found in body of HTML
			addressElementId: 'address-[[id]]',	
			// Source element id which contains destination address text
			mapElementId: 'map-container-[[id]]',
			route: [[loc.route]]
			// true: prompt user location, and route to destination address. 
		});
	</script>
	
Properties
  
	[
	    {
	        "element": {
	            "name": "Map of destination",
	            "properties": [
	                {
	                    "property": {
	                        "name": "What is the address?",
	                        "value": "360 Collins Street, Melbourne",
	                        "type": "Text",
	                        "reference": "address"
	                    }
	                },
	                {
	                    "property": {
	                        "name": "Show route to the Person?",
	                        "value": "false",
	                        "type": "Text",
	                        "reference": "route"
	                    }
	                }
	            ],
	            "reference": "loc"
	        }
	    }
	]

Scripts

	[
	    "http://content.whispir.com/public/template/lib/plugins/v1.6.js"
	]
	
## Conditional Logic

Conditional logic allows content to be dynamically shown or hidden based on the presence of a value in a supplied variable, or field. This hidden content would be visible to the template author but hidden from the message recipient.

### How conditional logic works

### Logic / functional operators

#### if
This basic conditional operator is used to test if an attribute has any value. If this attribute has a value, it returns content specified within this block.

	{{#if @@attribute@@}} exists and has content {{/if-cond}}
#### if-cond

Conditional operator used to perform a string comparison of an attribute's value. If true, returns content specified within block.

	{{#if-cond @@attribute@@ '==' 'true'}} Yes, it's true {{/if-cond}}

**if-cond** supports, '==' equal to, and '!=' not equal to.

#### each

Iterator used to traverse through an object or array. Returns access to child attributes within block. Order is preserved, no sort.

	{{#each @@manifest@@}} @@timestamp@@ - @@note@@ {{/each}}

### Limits of conditional logic

* All attributes values will be either a String type, or an Object of strings type.
* Conditional logic will only support direct string comparisons.

### Conditional logic example

#### Sample attribute data

	[{
	 "fullname": "Franco Trimboli", 
	 "email": "ftrimboli@whispir.com", 
	 "mobile": "0410509001", 
	 "num_days": "4", 
	 "workcentre_name": "Hawthorn", 
	 "new_customer": "true", 
	 "addressee_only": "false", 
	 "manifest": 
	  [{
	   "name": "Job Manifest",
	   "value": [{"timestamp":"20-10-2014 10:15","note":"Req. Start Time"},
	             {"timestamp":"21-10-2014 16:00","note":"End Time"}] 
	  }]
	}]

#### Sample conditional logic in template (plain email shown here)

	Hi @@fullname@@, 
	
	You have an job to process within @@num_days@@ 
	days at @@workcentre_name@@. 

	{{#if-cond @@new_customer@@ '==' true}} 
	See the check-in desk on arrival.
	 {{/if-cond}}

	{{#if-cond @@addressee_only@@ '==' true}} 
	Addressee only. 
	{{/if-cond}}

	{{#if @@id_required@@ }} 
	ID required. 
	{{/if}}

	Details:
	{{#each @@manifest@@}}
	@@timestamp@@ - @@note@@
	{{/each}}

	See @@web_url@@ for more.

#### Output

	Hi Franco Trimboli, 
	
	You have an job to process within 4 days at Hawthorn. 
	See the check-in desk on arrival.
	
	Details:
	20-10-2014 10:15 - Req. Start Time
	20-10-2014 16:00 - End Time
	
	See http://customer.au.whispir.com/s/aYid781 for more.



