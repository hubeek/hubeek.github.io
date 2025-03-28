# List example

_Status: Published_
_Created: 2019-06-11 14:04:22_
_Tags: swiftUI_

From RW:
[Ray Wenderlich Video Tut](https://www.raywenderlich.com/3779270-swift-ui-declarative-ui)
<code>
import PlaygroundSupport
import SwiftUI
struct Employee: Identifiable {
    var id = UUID()
    var name: String
    var title: String
}

let testData: [Employee] = [Employee(name: "Ray Wenderlich", title: "Owner"),
                            Employee(name: "Victoria Wenderlich", title: "Digital Artist"),
                            Employee(name: "Andrea Lepley", title: "Video Team Lead"),
                            Employee(name: "Sam Davies", title: "CTO"),
                            Employee(name: "Katie Collins", title: "Customer Support Lead"),
                            Employee(name: "Tiffani Randolph", title: "Marketing Associate")]

struct ContentView: View {
    var employees:[Employee] = []
    
    var body: some View {
        
            List(employees) { employee in
                NavigationButton(destination: Text(employee.name)) {
                    VStack(alignment: .leading) {
                        Text(employee.name)
                        Text(employee.title).font(.footnote)
                    }
                }
            }.navigationBarTitle(Text("Ray's Employees"))
        
    }
}
let vc = UIHostingController(rootView: NavigationView() { ContentView(employees: testData)})

PlaygroundPage.current.liveView = vc

</code>