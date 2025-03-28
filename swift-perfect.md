# Swift Perfect

_Status: Published_
_Created: 2017-04-28 02:53:53_
_Tags: swift_

<code>
mkdir hjh
cd hjh
swift package init --type executable
swift package generate-xcodeproj
open ./hjh.xcodeproj/
</code>

edit package.swift
<code>
import PackageDescription
let package = Package(
  name: "hjh",
  dependencies: [
    .Package(url: "https://github.com/PerfectlySoft/Perfect-
HTTPServer.git", majorVersion: 2),
    .Package(url: "https://github.com/SwiftORM/SQLite-StORM.git",
majorVersion: 1, minor: 0),
    .Package(url: "https://github.com/PerfectlySoft/Perfect-
Mustache.git", majorVersion: 2),
] )
</code>

terminal:
<code>
swift package update
swift package generate-xcodeproj
</code>

main.swift:
<code>
import PerfectLib
import PerfectHTTP
import PerfectHTTPServer
</code>

terminal:
<code>
mkdir public
touch public/file.txt
swift package generate-xcodeproj
</code>

terminal:
<code>
mkdir public
touch public/file.txt
swift package generate-xcodeproj
</code>

<code>
let server = HTTPServer()
server.serverPort = 8080
server.documentRoot = "public"

do {
  try server.start()
} catch PerfectError.networkError(let err, let msg) {
  print("Network error thrown: \(err) \(msg)")
}

// func for fitst json response
func jsonresponsefunc(request: HTTPRequest, response: HTTPResponse) {
  do {
    try response.setBody(json: ["message": "JSON!"])
      .setHeader(.contentType, value: "application/json")
      .completed()
  } catch {
    response.setBody(string: "Error handling request: \(error)")
      .completed(status: .internalServerError)
  }
}
// routes
var routes = Routes()
routes.add(method: .get, uri: "/", handler: jsonresponsefunc)
server.addRoutes(routes)
</code>