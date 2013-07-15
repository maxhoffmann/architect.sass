architect.sass
==============

architect.sass is a sass mixin library which aims to abstract the positioning of elements. It doesn’t add any classes to the compiled CSS and uses when-undo-mixins for easier responsive styling.

HOW DOES IT WORK?
-----------------

__Example 1: centering elements__

	.widget
		+when('min-width: 400px')
			+center('.widget-title', horizontally)
		+when('min-width: 600px')
			+undo-center('.widget-title', horizontally)
			+center('.widget-title', vertically)

__Example 2: rows__

	.gallery
		+row('.image')
		+when('max-width: 400px')
			+undo-row('.image')
				+center-horizontally

__Example 3: media object && flag object__

	.media
		+media('.media-img', '.media-body')

	.flag
		+media(img, p, left-middle) // you can also use tags instead of classes

__Example 4: drop caps__

	.article
		+drop-cap
			font-size: 3em
			background-color: #eee
		+when('min-width: 500px')
			+drop-cap-to-middle

___NOTE:___ There is an example page included in the repository.

CONVENTIONS
-----------

Mixins can be removed with the "undo-" mixin, e.g.

	.foo
		+center('.bar') // centers .bar inside of .foo

		+when('min-width: 400px')
			+undo-center('.bar') // remove styles that have centered .bar

Mixins with __one__ element in their parameters may style the specified element directly, e.g.

	+center('.foo')
		color: blue

Most mixins can extend their styles. Simply add true as the last argument to share those styles between multiple classes.

	.widget1
		+center('.widget-title', horizontally, true)

	.widget2
		+center('.widget-title', horizontally, true)

	// compiles to

	.widget1,
	.widget2 {
		text-align: center;
		vertical-align: top;
	}
	.widget1 > .widget-title,
	.widget2 > .widget-title {
		display: inline-block;
	}

You can use the "and" mixin for more syntactic sugar when chaining media queries.

	.header
		+when('min-width: 400px')
			+and('max-width: 600px')
				color: blue

__or__

	+when('min-width: 400px')
		+and('max-width: 600px')
			.header
				color: blue
