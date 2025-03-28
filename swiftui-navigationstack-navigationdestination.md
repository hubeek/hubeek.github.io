# SwiftUI NavigationStack + NavigationDestination

_Status: Published_
_Created: 2023-03-11 05:37:12_

## How NOT to implement the new NavigationStack NavigationDestination

```
import SwiftUI

struct ContentView: View {
    let arrayNums = [
        LItem(name: "1"),
        LItem(name: "2"),
        LItem(name: "3")
    ]
    var body: some View {
        NavigationStack {
            List{
                ForEach(arrayNums) { litem in
                    NavigationLink("nav link \(litem.name)", value: litem)
                }.navigationDestination(for: LItem.self) { tview in
                    TView(text: tview.name)
                }
            }
            
        }
    }
}

struct LItem: Codable, Equatable, Identifiable, Hashable {
    var id = UUID().uuidString
    let name: String
}
struct LView: View {
    var body: some View {
        TView(text: "in lview")
    }
}
struct TView: View {
    var text: String
    init(text: String) {
        print("init Tview \(text)")
        self.text = text
    }
    var body: some View {
        Text("\(text)")
    }
}

```
when opening the first link... All links are opened/instantiated?  
All the links are added to the navigationstack and loaded?  
log:  
```
init Tview 3
init Tview 2
init Tview 1
init Tview 3
init Tview 2
init Tview 1
init Tview 3
init Tview 2
init Tview 1
```
when pushing the back button you will navigate to Tview 2 and TView 3?   
seems like the assumption that all the links are in the nav stack and loaded is right..  

ChatGPT solution is to step away from the new navigationstack/destination:   
```
struct ContentView: View {
    let arrayNums = [        LItem(name: "1"),        LItem(name: "2"),        LItem(name: "3")    ]
    var body: some View {
        NavigationView {
            List {
                ForEach(arrayNums) { litem in
                    NavigationLink(
                        destination: TView(text: litem.name),
                        label: {
                            Text("nav link \(litem.name)")
                        })
                        .id(litem.id) // use id to force SwiftUI to create a new instance of TView
                }
            }
        }
    }
}
```
the logging will display now only:  
```
init Tview 1
init Tview 1
init Tview 2
init Tview 2
init Tview 3
init Tview 3
```

This must be from the List component. When adding a .omAppear with text the log shows:  

```
init Tview 1
init Tview 1
init Tview 2
init Tview 2
init Tview 3
init Tview 3
TView with text 1 appeared
```
