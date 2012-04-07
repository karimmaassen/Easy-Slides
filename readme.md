## Schedule

I plan to being working on this May 1st. Pull requests or discussion is hugely welcomed!

## Goal

Creating slides takes time - a lot of time. For the coders among us, I want to change that. In fact, I want to make it as simple as humanly possible to generate a beautiful presentation, using nothing but a bit of JSON. 

Here's an example of the shape of the final product.

```html
<script>
{
	"presentation": {
		"title": 'My Great Presentation',

		"slides": [

			// slide 1
			{
				"title": 'Learn About Borders',
				"bullets": [
					'Thing 1',
					'Thing 2',
				],
				"code": ['path/to/file.css', [2,4]] // path to file, lines to grab
			},
			
			// slide 2 
			{
				"title": 'Learn About Margins',
				"quote": 'Always remember bla bla',
				"transition": 'fade' // optionally specify transitions
			}, 

			// slide 3
			{
				"title": 'Learn About Things',
				"body": 'Description that goes below the "title"',
				"code": ['path/to/snippet', [0,3]] // path, lines
			}, 

			// slide 4
			{
				"title": 'Learn About Whatever',
				"image": 'path/to/image.jpg'
			}
		]
	}
}
</script>
```

This way, developers can create a handful of object literals, and forget about worrying about spacing, alignment, animation, interaction, etc. Consider the first slide:

```html
{
	"title": 'Learn About Borders',
	"bullets": [
		'Thing 1',
		'Thing 2',
	],
	"code": ['path/to/file.css', [2,4]] // path to file, lines to grab
}
```

This specifies that:

- The slide should have a title of "Learn About Borders"
- There will be two bullets - each which is activated/displayed in ordered, when the speaker presses the space bar.
- A sample block of code from `file.css`. Only lines 2-4 from that file will be displayed in the slide.

Once this code is provided, that's all the presenter needs to do. Behind the scenes, the objects will be bound to a template, and the keyboard events/animations/interactions will be prepared. I literally want the JSON to be the _only_ step required.

## Options

There should be a variety of different slide-styles, such as a large quote, an image, a bulleted list, etc. Here's what I'm thinking at this point:

- *Image* - Simple slide with vertically/horizontally centered image
- *Bullets* - The defacto slide. Contains bullets and code blocks
- *Quote* - A nicely styled quote
- *Web View* - Pass a URL, and the slide loads an iframe of the web page.

I'm thinking that the user may need to specify the type of slide in the code (which I have not outlined in the sample code above). What if they try to include both quotes and images? This will break the formatting. They may need to do: `{ type: 'bullets', ...}`. 

## Advantages

There's a variety of advantages to creating presentations in this fashion:

- Presentations can easily be styled/modified. You only need to update a stylesheet.
- Get your mind out of Keynote, and back into your presentation. Add a few key value pairs, and, bam, your slide is ready to go.
- Way faster than any alternative
- Load your presentation as easy as $.getJSON('presentation.js')
- Because we're using JSON, creating a presentation-generator UI for non-coders is a much easier process

## Usage

The idea is that the styling/template is already in place. So I'd imagine that the presenter will only need to do something like:

		var slides = $.getJSON('presentation.js');
		new Presentation( slides, config );

(Not set in stone; still need to think about this.)

## Tools

As for the tools in this project, I'd like to use:

- *Library* - jQuery (Or maybe just stick with Underscore)
- *Framework* - Backbone.js
- *Testing* - QUnit
- *CSS* - Sass (I prefer Stylus, but Sass is more common)