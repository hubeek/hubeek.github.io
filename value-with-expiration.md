# Value with expiration

_Status: Published_
_Created: 2019-06-07 05:40:14_
_Tags: iOS swift_

<code>
@propertyWrapper
struct Expirable<Value> {
    let duration: TimeInterval
    var expirationDate: Date = Date()
    private var innerValue: Value?
    
    var value: Value? {
        get{ return hasExpired() ? nil: innerValue }
        set{
            self.expirationDate = Date().addingTimeInterval(duration)
            self.innerValue = newValue
        }
    }
    init(duration: TimeInterval) {
        self.duration = duration
    }
    private func hasExpired() -> Bool {
        return expirationDate < Date()
    }
}

struct Tokens {
    @Expirable(duration: 3) static var authent: String
}

Tokens.authent = NSUUID().uuidString

sleep(2)
Tokens.authent ?? "token has expired"
sleep(2)
Tokens.authent ?? "token has expired"
</code>