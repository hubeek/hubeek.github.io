# Switch Language HTML query

_Status: Published_
_Created: 2016-06-11 08:55:54_
_Tags: javascript query_

script.js

<code>
//switch language

$( "img" ).click(function() 
{
 $( "div.languageselect" ).toggle();
  var _this = $(this);
      var current = _this.attr("src");
      var swap = _this.attr("data-swap");     
     _this.attr('src', swap).attr("data-swap",current);
});
</code>

html

<code>
<!doctype html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<title>Switch Languages</title>
	<meta name="description" content="Switch Languages">
	<meta name="author" content="huh.snips.nl">
</head>

<body>

	<img src="assets/images/englishflag.png" data-swap="assets/images/dutch.jpg" class="languageselect" alt="Mountain View" style="width:40px;height:22px;">
	<div class="languageselect">English</div>
	<div class="languageselect" style="display: none">Nederlands</div>

	<script src="assets/js/jquery-2.1.3.min.js"></script>
	<script src="assets/js/jquery.actual.min.js"></script>
	<script src="assets/js/script.js"></script>
</body>
</html>
</code>