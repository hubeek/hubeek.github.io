# prevent update to mojave

_Status: Published_
_Created: 2018-11-05 05:30:25_
_Tags: mac_

in /Library/Bundles/
then move it to doc folder and turn off

<code>
sudo mv /Library/Bundles/OSXNotification.bundle ~/Documents/ && softwareupdate --ignore macOSInstallerNotification_GM
</code>

turn back
move it back to /Library/Bundles/
<code>
softwareupdate --reset-ignored
</code>