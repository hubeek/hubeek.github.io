# Navigation link button makes master detail setup on iPad 

_Status: Published_
_Created: 2019-10-12 12:13:20_
_Tags: swiftUI, swift_

.navigationViewStyle(StackNavigationViewStyle()) does the trick...
<code>
NavigationView {
        Text("Hello world!")
    }
    .navigationViewStyle(StackNavigationViewStyle())
</code>