# Leaner Susy Breakpoints

Susy is an awesome responsive grid framework built on SASS, <a href="susy.oddbird.net">susy.oddbird.net</a>

It has a few IE fallback mixins but I wasn't really happy with their output since for older browsers, they rely on a fallback class being supplied and appended to the selector.  I usually provide an IE-specific stylesheet for responsive sites, so this extra step is redundent and just adds bloat. Yes, CSS performance is probably the last thing we need to think about, practically speaking, but I'm not 100% convinced and again, just hate that extra class

Also, to use the fallback, the class parameter must be provied to the `at-breakpoint` mixin, and because of a SASS issue, this won't work if the mixin is called on the document root <a href="https://github.com/ericam/susy/issues/26">https://github.com/ericam/susy/issues/26</a>

So, what follows below may be totally unnecessary, but instead of using the default "at-breakpoint" with fallback class supplied by Susy, I just created a wrapper of sorts to spit out the query contents in IE7/8 stylesheets.