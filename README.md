# Leaner Sass Media Query Breakpoints

Responsive design and development is here to stay, but how should we organize our CSS for older browsers that may not yet support the (not really new anymore) hotness?

This is especially important in mobile-first design/development, where a lot of desktop styles may be defined inside of `min-width` MQ's that wouldn't be picked up in IE8. Plus, chances are we don't want our IE8 page to look like the mobile version of the site... so defaulting to the mobile styles isn't the best option either.

Libraries like Breakpoint <a href="http://breakpoint-sass.com/"> are awesome and have a few IE fallback mixins built in, but they still result in a lot of wasted code being generated for IE8 stylesheets. Breakpoint for example provides a handy way to supply a fallback class and style for non-responsive browsers, but both the responsive & fallback styles <a href="http://breakpoint-sass.com/#advanced">get added</a> to the stylesheet. The end result works, but I hate the idea of an IE8 stylesheet still receiving a bunch of styles that are immediately over-written by the fallbacks. It just adds bloat and makes the generated sheet have that much greater a filesize.

So, I've started using a helper on top of the `@include breakpoint()` to help me out. This is all based off <http://jakearchibald.github.io/sass-ie/>, so not a lot of new stuff here. I'm just applying it on top of Breakpoint's great mixins.

First, I create a non-responsive application-level stylesheet that I include inside old-school browsers and set a few config vars to `true`. Now, inside my Sass partials, I call the `breakpoint` mixin with an extra boolean argument specifying if its styles should be added to the oldIE stylesheet or not. If I pass true, the style will show up in the oldIE stylesheet unwrapped from a media query. If false, they'll be ignored and only show up in my responsive stylesheet. This way, I can include the useful styles and ignore the responsive "cruft".


      @include lean-breakpoint($breakpoint, $includedInIE) {
        //styles
      }

      $breakpoint is your breakpoint... ie "600px"
      $includedInIE is a flag of whether or not to include the style in your IE stylesheet. Defaults to FALSE
      Anything that's meant for just mobile or tablet you'd leave alone, anything that applies to a desktop or default styles, you'd pass in true.

Modern browsers get media query styles, without any IE-hack pollution.  Old IE sheets only see non-media-query styles and any additional styles for IE fixes.  Everyone's a winner.
