# Git foreach use cases

_Status: Published_
_Created: 2019-08-13 03:54:39_
_Tags: git, terminal_

What did I do before the holidays?
<code>
git for-each-ref --count=30 --sort=-committerdate refs/heads/ --format='%(refname:short)'
</code>

sort by date
<code>
git for-each-ref --sort=-committerdate refs/heads/
</code>