# Operationqueue urlsession

_Status: Published_
_Created: 2020-02-04 13:02:47_
_Tags: swift, concurrent, network, dispatch_

<code>

let group = DispatchGroup()
for _ in 0...999 {
    group.enter()
    URLSession.shared.dataTask(with: …) { _, _, _ in
        …
        group.leave()
    }.resume()
}
group.wait()

</code>