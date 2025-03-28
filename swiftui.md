# SwiftUI

_Status: Published_
_Created: 2019-06-11 03:08:45_
_Tags: Swift SwiftUI_

Playground
```
import PlaygroundSupport
import SwiftUI


struct ContentView: View {
    var body: some View {
        Text("Hello World")
    }
}
let vc = UIHostingController(rootView: ContentView())

PlaygroundPage.current.liveView = vc
```


###Shapes###
```
Rectangle()
    .fill(Color.red)
    .frame(width: 200, height: 200)
Circle()
    .fill(Color.blue)
    .frame(width: 50, height: 50)
```
Try HStack en ZStach(!)


###Triangles Shapes###
```
struct ASymbol : View {
    let symbolColor: Color
    
    var body: some View {
        GeometryReader { geometry in
            Path { path in
                let side = min(geometry.size.width, geometry.size.height)
                path.move(to: CGPoint(x: side * 0.5, y: 0))
                path.addLine(to: CGPoint(x: side, y: side))
                path.addLine(to: CGPoint(x: 0, y: side))
                path.closeSubpath()
                
                }
                .fill(self.symbolColor)
        }
    }
}
struct ContentView : View {
    var body: some View {
        VStack{
        ASymbol(symbolColor: .green)
        ASymbol(symbolColor: .green).rotationEffect(Angle(degrees: 180))
        }
    }
}
```
Conditional:
```
struct ContentView: View {
    var body: AnyView {
        if Int.random(in: .min ... .max).isMultiple(of: 2) {
            return AnyView(Text("Even"))
        } else {
            return AnyView(Image(systemName: "star"))
        }
    }
}
```