# <img src="https://raw.githubusercontent.com/norganna/marked-usermacro/master/marked.png" title="marked-usermacro" height="30px"> Marked User Macro for Confluence.
User macro to allow GitHub flavoured markdown blocks inside Confluence pages via marked.js.

## Description
This macro is designed to render the markdown body content in the page whilst preserving the original markdown code in the macro body, so that consequential edits of the page can update the markdown code.
The markdown code is rendered at page display time by the [marked.js](https://github.com/chjj/marked) javascript library.

## Installation
Add the following to your user macros page, which you can find by:
* going to the **Configuration** page as an administrator 
* selecting **User Macros** in the left navigation panel (in the **Configuration** block)
* navigating to **Create a User Macro** page
* entering the **Information** and **Definition** as per the comments at the top of the following code
* pasting the code into the **Template** text box

## Code
```
## Macro name: marked
## Macro title: Marked markdown content
## Categories: Formatting
## Description: Display markdown content in Github flavoured markdown via the marked.js engine.
## Visibility: to all users
## Icon URL: https://raw.githubusercontent.com/norganna/marked-usermacro/master/marked.png
## Documentation URL: https://help.github.com/articles/github-flavored-markdown/
## Macro has a body: Y
## Body processing: Unrendered
## Generates: HTML
##
## @noparams
##
## Developed by: Ken Allan (https://github.com/norganna)
## Date created: 2015-09-01

#set ($randomId="")
#macro(getRandomId)
#set ($string="")
#set ($rand=$string.class.forName("java.util.Random").getConstructor().newInstance())
#set ($randomId=$rand.nextInt(2147483647).toString())
#end
#getRandomId()

<div id="markedcontent_$randomId">
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js">
</script>
<script>
jQuery(function() {
    jQuery('#markedcontent_$randomId').html(marked($jsonator.convert($body).serialize(),{
        gfm: true,
        tables: true,
        breaks: false,
        pedantic: false,
        sanitize: true,
        smartLists: true,
        smartypants: false
    }));
});
</script>
```

## Usage
This code is safe to include multiple times per page.
Include on your confluence page by using the `{marked}` tag like this:

```markdown
{marked}
# Head 1
## Head 2
Content content.

* List item 1
* List item 2
{marked}
```

## License

Copyright 2015, Ken Allan, MIT License.

See LICENSE file for more information.
