# Dispatch async

_Status: Published_
_Created: 2018-05-04 04:18:04_
_Tags: iOS_

<code>
DispatchQueue.global(qos: .background).async {
    // Background Thread
    DispatchQueue.main.async {
        // Run UI Updates or call completion block
    }
}

Main and Background Queues

let main = DispatchQueue.main
let background = DispatchQueue.global()
let helper = DispatchQueue(label: "another_thread") 
Working with async and sync threads!

 background.async { //async tasks here } 
 background.sync { //sync tasks here } 
</code>