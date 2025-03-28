# Pool

_Status: Published_
_Created: 2016-12-01 15:33:38_
_Tags: swift_

<code>
class Pool<T> {
    private var objectPool = [T]()
    
    init(items:[T]) {
        objectPool.reserveCapacity(objectPool.count)
        for item in items {
            objectPool.append(item)
        }
    }
    
    func getFromPool() -> T? {
        var result:T?
        if objectPool.count > 0 {
            result = self.objectPool.removeAtIndex(0)
        }
        return result
    }
    
    func returnToPool(item:T) {
        self.objectPool.append(item)
    }
}
</code>