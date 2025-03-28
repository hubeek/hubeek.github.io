# SwiftUI Elements

_Status: Published_
_Created: 2019-06-11 05:07:42_
_Tags: swiftUI, swift_

## Text##
`Text("Hello World!")`
```
Text("Hello World")
    .font(.largeTitle)
    .foregroundColor(Color.green)
    .lineSpacing(50)
    .lineLimit(nil)
    .padding()
```
multiline
```
Text("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse est leo, vehicula eu eleifend non, auctor ut arcu")
      .lineLimit(nil).padding()
```
```
struct ContentView: View {
    static let dateFormatter: DateFormatter = {
        let formatter = DateFormatter()
        formatter.dateStyle = .short
        return formatter
    }()
    
    var now = Date()
    var body: some View {
        Text("Now is the Date: \(now, formatter: Self.dateFormatter)")
    }
}
```
## Text with background##
```
Text("Hello World").color(.red).font(.largeTitle).background(Image(systemName: "photo").resizable().frame(width: 100, height: 100))
```
## Images ##
sytem icon images
```
Image(systemName: "photo")
            .foregroundColor(.red)
            .font(.largeTitle)
Image(systemName: "star").resizable().aspectRatio(contentMode: .fill).padding(.bottom)
```

cast from UIImage to Image
```
if let image = UIImage(named: "test.png") {
  Image(uiImage: image)
}
```
#Stacks#
HStack, VStack, ZStack
with styling:
```
VStack (alignment: .leading, spacing: 20){
    Text("Hello")
    Divider()
    Text("World")
}
```
on top of each other:
```
ZStack() {
    Image("hello_world")
    Text("Hello World")
        .font(.largeTitle)
        .background(Color.black)
        .foregroundColor(.white)
}
```
#Input#
##Toggle##
@State var isShowing = true //state
```
Toggle(isOn: $isShowing) {
    Text("Hello World")
}.padding()
```
##Button##
```
struct ContentView : View {
  var body: some View {
  
    Button(action: {
        self.buttonPress()
      }, label: {
          Text("TickTock").color(.white)
      }).frame(minWidth: 0, maxWidth: .infinity)
        .padding(20)
        .background(Color.blue)
  }
  
  private func buttonPress() {
    print("tick tock")
  }
    
}

```
###(new!) to next view with presentation button###
```
struct NextView: View {
  var body: some View {
    Text("NextView")
  }
}

struct ContentView : View {
  var body: some View {
  
    PresentationButton(Text("Navigate to another View"), destination: NextView())
  }
}
```