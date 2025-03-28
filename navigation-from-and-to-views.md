# Navigation from and to views

_Status: Published_
_Created: 2024-03-22 08:09:05_
_Tags: iOS, Swift SwiftUI_

```swift
struct ContentView: View {
    @State private var selection: Int? = 0

    var body: some View {
        NavigationView {
            VStack {
                if selection == 0 {
                    FirstView(selection: $selection)
                } else if selection == 1 {
                    SecondView(selection: $selection)
                } else if selection == 2 {
                    ThirdView(selection: $selection)
                }
            }
        }
    }
}

struct FirstView: View {
    @Binding var selection: Int?

    var body: some View {
        Button("Go to Second View") {
            selection = 1
        }
    }
}

struct SecondView: View {
    @Binding var selection: Int?

    var body: some View {
        Button("Go to Third View") {
            selection = 2
        }
    }
}

struct ThirdView: View {
    @Binding var selection: Int?

    var body: some View {
        Button("Go to First View") {
            selection = 0
        }
    }
}



#Preview {
    ContentView()
}
```