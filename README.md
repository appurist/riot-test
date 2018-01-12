# riot-test
Just a quick experiment with Riot.js to check out components, nested components, parameters and yields.

It is very light, does not require anything like browserify or webpack, and this example compiles the custom tags on demand.

To try the code, just copy the files to a web server somewhere, or run `npm start` or `npm serve`.  All those commands do is run http-server on the local folder to serve the files.

In this example, `index.html` just defines this HTML text:
```
    <sample>Sample #1</sample>
    <sample>Sample #2</sample>
```
These `<sameple>` tags reference a custom `sample.tag` file which defines a more complex component, and also displays the text value
contained within the tag as the yield within an `<h3>` header, along with another data item named `subheading` provided by (and local to) the component:
```
<sample>
  <h3> <yield /> </h3>
  <h5>{subheading}</h5>
```
It then defines a list, iterating over `items` and passing each of those to a `<nested>` component as `param`:
```
  <ul>
    <nested each={ items } param="{name}">{ name.toUpperCase() }</nested>
  </ul>
```
It also demonstrates the use of arbitrary Javascript code within a template, within a pare of braces, 
which places the uppercase version of the name within the tag payload (yield).

The `<nested>` component (defined in `nested.tag`) provides this as an `<li>` value for the list:
```
  <li>param=<b>{opts.param}</b> as a yield in uppercase is <b><yield /></b> </li>
```
Note there are two copies of the `<sample>` component, referenced in the `index.html` page.  
The resulting web page looks like this (with a bit of CSS added):

![output from index.html](https://i.gyazo.com/d4f8c39641f6d50107fe7064947f22d7.png)

See the source code for more details.
