# Mutating Core Data object 

_Status: Published_
_Created: 2022-07-22 08:37:05_
_Tags: swift, swiftUI, coredata, iOS OSX max_

## Problem: How to mutate a fetched CD object in child views

```

import SwiftUI
import CoreData

struct ContentView: View {
    @Environment(\.managedObjectContext) private var viewContext

    @FetchRequest(
        sortDescriptors: [NSSortDescriptor(keyPath: \Item.timestamp, ascending: true)],
        animation: .default)
    var items: FetchedResults<Item>

    var body: some View {
        NavigationView {
            List {
                
                
                ForEach(items) { item in
                    NavigationLink {
                        ItemDetail(item: item)
                    } label: {
                        Text("itemview1 at \(item.timestamp!, formatter: itemFormatter) name: \((item.name ?? "").isEmpty ? "": item.name! )")
                    }

                }
                .onDelete(perform: deleteItems)
            }
            .toolbar {
#if os(iOS)
                ToolbarItem(placement: .navigationBarTrailing) {
                    EditButton()
                }
#endif
                ToolbarItem {
                    Button(action: addItem) {
                        Label("Add Item", systemImage: "plus")
                    }
                }
            }
            Text("Select an item")
        }
    }

    private func addItem() {
        withAnimation {
            let newItem = Item(context: viewContext)
            newItem.timestamp = Date()

            do {
                try viewContext.save()
            } catch {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                let nsError = error as NSError
                fatalError("Unresolved error \(nsError), \(nsError.userInfo)")
            }
        }
    }

    private func deleteItems(offsets: IndexSet) {
        withAnimation {
            offsets.map { items[$0] }.forEach(viewContext.delete)

            do {
                try viewContext.save()
            } catch {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                let nsError = error as NSError
                fatalError("Unresolved error \(nsError), \(nsError.userInfo)")
            }
        }
    }
}

private let itemFormatter: DateFormatter = {
    let formatter = DateFormatter()
    formatter.dateStyle = .short
    formatter.timeStyle = .medium
    return formatter
}()

struct ItemDetail: View {
    
    @ObservedObject var item: Item
    @State var name: String = ""
    
    var body: some View {
        Form {
            TextField("Enter name", text:  $name ).onChange(of: name) { newValue in
                item.name = name
            }
            Button("Submit") {
                // nav back
            }
            Spacer()
            NavigationLink {
                ItemDetail(item: item)
            } label: {
                Text("itemview1 at \(item.timestamp!, formatter: itemFormatter) name: \((item.name ?? "").isEmpty ? "": item.name! )")
            }
        }
    }
}
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView().environment(\.managedObjectContext, PersistenceController.preview.container.viewContext)
    }
}
```