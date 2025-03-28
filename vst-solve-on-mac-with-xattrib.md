# vst solve on mac with xattrib

_Status: Published_
_Created: 2022-05-26 04:55:31_

When Mac OSX is complaining about a vst  
### user  
```
sudo xattr -rd com.apple.quarantine /Users/<usrname>/Library/Audio/Plug-Ins/Components/Henrietta\ Smith-Rolla\ -\ Spectrum.vst3
```
### system
```
sudo xattr -rd com.apple.quarantine /Library/Audio/Plug-Ins/VST3/Henrietta\ Smith-Rolla\ -\ Spectrum.vst3
```