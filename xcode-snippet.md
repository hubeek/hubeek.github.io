# Xcode snippet

_Status: Published_
_Created: 2016-07-22 02:18:30_
_Tags: swift_

<h2>Code Snippet Library within Xcode</h2>
variable to edit is within <b><# var #></b>
<code>
// FIXME: <# Subject #>
</code>

<h2>to make todo / fix into warning</h2>
add run script in Build Phases
shell: /bin/sh
(tick 'Show environment variables in build log')
<code>
TAGS="TODO:|FIXME:"
find "${SRCROOT}" \( -name "*.h" -or -name "*.m" -or -name "*.swift" \) -print0 | xargs -0 egrep --with-filename --line-number --only-matching "($TAGS).*\$" | perl -p -e "s/($TAGS)/ warning: \$1/"
</code>