# swift server Kitura

_Status: Published_
_Created: 2017-01-23 06:59:28_
_Tags: swift_

first
<code>
mkdir tuinhok
cd tuinhok
swift package init --type executable
</code>
adjust Package.swift
<code>
import PackageDescription


let package = Package(
  name: "proj1",
  dependencies: [
    .Package(url: "https://github.com/IBM-Swift/Kitura.git",
             majorVersion: 1),
    .Package(url: "https://github.com/IBM-Swift/HeliumLogger.git", majorVersion: 1),
    .Package(url: "https://github.com/IBM-Swift/Kitura-StencilTemplateEngine.git", majorVersion: 1)
    ]
)

</code>
swift package generate-xcodeproj
mkdir public - for js css img etc
mkdir Views - for stencil files
<br />
in main swift
<code>
import Kitura
import LoggerAPI
import HeliumLogger
import KituraStencil

HeliumLogger.use(.info)
let router = Router()
router.setDefault(templateEngine: StencilTemplateEngine())
router.all("/static", middleware: StaticFileServer())

router.get("/") {
  request, response, next in
  defer { next() }
  try response.render("home", context: [:])
}

Kitura.addHTTPServer(onPort: 8090, with: router)

Kitura.run()
</code>