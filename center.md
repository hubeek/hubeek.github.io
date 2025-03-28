# center

_Status: Published_
_Created: 2014-06-09 07:11:00_
_Tags: css_

<h2>Centering lines of text</h2>
<code>
P { text-align: center }
H2 { text-align: center }
</code>


<h2>Centering a block of text or an image</h2>

<code>
P.blocktext {
    margin-left: auto;
    margin-right: auto;
    width: 6em
}
...
<P class="blocktext">This rather...
</code>

<code>
IMG.displayed {
    display: block;
    margin-left: auto;
    margin-right: auto }
...
<IMG class="displayed" src="..." alt="..."></code>

<h2>Centering a block or an image vertically</h2>

<code>
DIV.container {
    min-height: 10em;
    display: table-cell;
    vertical-align: middle }
...
<DIV class="container">
  <P>This small paragraph...
</DIV>
</code>