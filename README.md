# sanitize-html

<a href="http://apostrophenow.org/"><img src="https://raw.github.com/punkave/sanitize-html/master/logos/logo-box-madefor.png" align="right" /></a>

`sanitize-html` provides a simple HTML sanitizer with a clear API.

`sanitize-html` is tolerant. It is well suited for cleaning up HTML fragments such as those created by ckeditor and other rich text editors. It is especially handy for removing unwanted CSS when copying and pasting from Word.

`sanitize-html` allows you to specify the tags you want to permit, and the permitted attributes for each of those tags.

If a tag is not permitted, the contents of the tag are still kept, except for script tags.

The syntax of poorly closed `p` and `img` elements is cleaned up.

`href` attributes are validated to ensure they only contain `http`, `https`, `ftp` and `mailto` URLs. Relative URLs are also allowed. Ditto for `src` attributes.

HTML comments are not preserved.

## Requirements

`sanitize-html` is intended for use with Node. That's pretty much it. All of its npm dependencies are pure JavaScript. `sanitize-html` is built on the excellent `htmlparser2` module.

## How to use

    npm install sanitize-html

    var sanitizeHtml = require('sanitize-html');

    var dirty = 'some really tacky HTML';
    var clean = sanitizeHtml(dirty);

That will allow our default list of allowed tags and attributes through. It's a nice set, but probably not quite what you want. So:

    // Allow only a super restricted set of tags and attributes
    clean = sanitizeHtml(dirty, {
      allowedTags: [ 'b', 'i', 'em', 'strong', 'a' ],
      allowedAttributes: {
        'a': [ 'href' ]
      }
    });

Boom!

"I like your set but I want to add one more tag. Is there a convenient way?" Sure:

    clean = sanitizeHtml(dirty, {
      allowedTags: sanitizeHtml.defaults.allowedTags.concat([ 'img' ])
    });

If you do not specify `allowedTags` or `allowedAttributes` our default list is applied. So if you really want an empty list, specify one.

"What are the default options?"

    allowedTags: [ 'h3', 'h4', 'h5', 'h6', 'blockquote',
    'p', 'a', 'ul', 'ol', 'nl', 'li', 'b', 'i', 'strong',
    'em', 'strike', 'code', 'hr', 'br', 'div',
    'table', 'thead', 'caption', 'tbody', 'tr', 'th', 'td',
    'pre' ],
    allowedAttributes: {
      a: [ 'href', 'name', 'target' ],
      // We don't currently allow img itself by default, but this
      // would make sense if we did
      img: [ 'src' ]
    },
    // Lots of these won't come up by default because
    // we don't allow them
    selfClosing: [ 'img', 'br', 'hr', 'area', 'base',
      'basefont', 'input', 'link', 'meta' ]

## Changelog

0.1.0:initial release.

## About P'unk Avenue and Apostrophe

`sanitize-html` was created at [P'unk Avenue](http://punkave.com) for use in Apostrophe, an open-source content management system built on node.js. If you like `sanitize-html` you should definitely [check out apostrophenow.org](http://apostrophenow.org). Also be sure to visit us on [github](http://github.com/punkave).

## Support

Feel free to open issues on [github](http://github.com/punkave/sanitize-html).

<a href="http://punkave.com/"><img src="https://raw.github.com/punkave/sanitize-html/master/logos/logo-box-builtby.png" /></a>
