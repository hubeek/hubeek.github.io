# Razor Snips

_Status: Published_
_Created: 2015-12-10 05:27:18_
_Tags: .net_

<h2>Send to Action Controller from checkbox</h2>
<code>
@Html.CheckBox("FilterOnDates", new { OnChange = "document.forms[0].submit();" })
</code>