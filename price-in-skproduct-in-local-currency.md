# price in SKProduct in local currency

_Status: Published_
_Created: 2018-03-01 06:13:45_
_Tags: iOS swift_

<code>
func priceStringForProduct(item: SKProduct) -> String? {
        let price = item.price
        if price == 0 {
            return "Free!" //todo: Translate
        } else {
            let numberFormatter = NumberFormatter()
            let locale = item.priceLocale
            numberFormatter.numberStyle = .currency
            numberFormatter.locale = locale
            return numberFormatter.string(from: price)
        }
    }
</code>