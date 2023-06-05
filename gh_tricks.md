# Some tricks to make this page work

## Obfuscate mailto links

To make life hard for spambots mailto links should not be plain text in the html code. I use a combination of tricks to hide the ral mail address from them:

- UTF encode all letters
  Instead encoding just special characters the whole email can be encoded. Use tools like [dencode.com](https://dencode.com/string). Take the 'unicode escape' result andreplace e.g. `\u00` with `%` to make it a valid URL.
- scrumble the mailto link with some css

Combined an example can look like this:

```html
<style>
  :root {
    --mydom: "web.net";
  }
  .at:before {
    content: "@";
  }
  .dom:after {
    content: var(--mydom);
  }
</style>
<a href="mailto:%68%65%6c%6c%6f%2e%77%6f%72%6c%64%40%77%65%62%2e%6e%65%74">
  hello.world
  <span class="at"></span>
  <span class="dom"></span>
</a>
```

resulting in

<style>
  :root {
    --mydom: "web.net";
  }
  .at:before {
    content: "@";
  }
  .dom:after {
    content: var(--mydom);
  }
</style>
<a href="mailto:%68%65%6c%6c%6f%2e%77%6f%72%6c%64%40%77%65%62%2e%6e%65%74">
  hello.world
  <span class="at"></span>
  <span class="dom"></span>
</a>

## Embedded maps

Github pages only allows some jekyll **plugins** and also blocks **iframes**. This makes including interactive maps hard. One workaround I found is to compile a version with the desired plugin (jekyll-leaflet) locally and then take the HTML part as a 'include'. Just place the html file in the \_includes folder and use it in your markdown with `{% include mymap.html %}`.
