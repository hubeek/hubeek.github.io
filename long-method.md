# Long method

_Status: Published_
_Created: 2018-12-11 01:58:29_
_Tags: iOS, swift_

<code>
func async(_ runner: @escaping @autoclosure () ->())
{
    DispatchQueue.global(qos: .default).async {
        runner()
    }
}

func longMethod() {
    for _ in 1...2 {
        sleep(5)
    }
    print("run like a boss")
}
async(longMethod())
</code>