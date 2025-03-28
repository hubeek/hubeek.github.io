# Spotlight

_Status: Published_
_Created: 2020-10-05 03:42:24_
_Tags: macOS, mac, terminal_

problems with indexing , not indexing, stopped indexing.

1)
<ul>
<li>
Enable Indexing – sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist</li>
<li>
Disable Indexing – sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist</li>
</ul>
2)
Open Terminal
Type - not copy! - the following but wait a few second between them:
<code>
sudo mdutil -i off /
sudo mdutil -i on /
sudo mdutil -E /
</code>
If, after a few minutes, Spotlight is still not indexing, try running this command, followed by the three commands above:
<code>
sudo rm -rf /.Spotlight-V100
</code>