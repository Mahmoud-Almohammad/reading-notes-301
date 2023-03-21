# EJS

## What is EJS?

EJS is a simple templating language that lets you generate HTML markup with plain JavaScript.

## Features

1. Fast compilation and rendering
2. Simple template tags: `<% %>`
3. Custom delimiters (e.g., use `[? ?]` instead of `<% %>`)
4. Sub-template includes
5. Ships with CLI

## Install

    $ npm install ejs

## Use

    let ejs = require('ejs');

## Tags

- `<%` 'Scriptlet' tag, for control-flow, no output

- `<%_` ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it

- `<%=` Outputs the value into the template (HTML escaped)

- `<%-` Outputs the unescaped value into the template

- `<%#` Comment tag, no execution, no output
- `<%%` Outputs a literal '<%'

- `%>` Plain ending tag

- `-%>` Trim-mode ('newline slurp') tag, trims following newline

- `_%>` ‘Whitespace Slurping’ ending tag, removes all whitespace after it

## Includes

Includes are relative to the template with the `include` call. (This requires the 'filename' option.) For example if you have "./views/users.ejs" and "./views/user/show.ejs" you would use `<%- include('user/show'); %>`.

You'll likely want to use the raw output tag (`<%-`) with your include to avoid double-escaping the HTML output.

    <ul>
    <% users.forEach(function(user){ %>
        <%- include('user/show', {user: user}); %>
    <% }); %>
    </ul>

## Custom delimiters

Custom delimiters can be applied on a per-template basis, or globally:

    let ejs = require('ejs'),
        users = ['geddy', 'neil', 'alex'];

    // Just one template
    ejs.render('<?= users.join(" | "); ?>', {users: users},
        {delimiter: '?'});
    // => 'geddy | neil | alex'

    // Or globally
    ejs.delimiter = '$';
    ejs.render('<$= users.join(" | "); $>', {users: users});
    // => 'geddy | neil | alex'

## Want more details? read [EJS][1]. 

[1]: <https://ejs.co/>
