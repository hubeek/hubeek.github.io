# Server side Swift

_Status: Published_
_Created: 2017-09-18 02:48:51_
_Tags: swift_

<H1>Kitura</h1>
mkdir serverside
cd serverside/
mkdir server
cd server
docker run -itv $(pwd):/projects --name projects -w /projects -p 8089:8089 -p 8090:8090 -p 5984:5984 twostraws/server-side-swift /bin/bash
docker start projects
docker attach projects
root@c661e0faa890:/projects# mkdir project1
root@c661e0faa890:/projects# cd project1/
root@c661e0faa890:/projects/project1# swift package init --type executable
root@c661e0faa890:/projects/project1# swift build
root@c661e0faa890:/projects/project1# .build/debug/project1
Hello, world!


change package to:
let package = Package(
    name: "project1",
    dependencies: [
    .Package(url: "https://github.com/IBM-Swift/Kitura.git", majorVersion: 1),
    .Package(url: "https://github.com/IBM-Swift/HeliumLogger.git", majorVersion: 1),
    .Package(url: "https://github.com/IBM-Swift/Kitura-StencilTemplateEngine.git", majorVersion: 1)
    ]
)

swift build
swift package generate-xcodeproj


docker ps - shows a list of running containers
docker ps -a  shows list all projects

docker start #NAME PROJ#
docker attach #NAME#
ctrl-p ctrl-q to get back to local terminal without stopping
docker start -i #NAME#

<H1>Vapor</h1>

Use & adjust Post template.
change in fluent.json 
"driver":"memory" into "driver":"sqlite"

create
sqlite.json
insert
{
    "path":"pokemonDB.sqlite"
}

in config+Setup
change setupPreparations into desired Pokemon class
<code>
private func setupPreparations() throws {
        preparations.append(Post.self)
        preparations.append(Pokemon.self)
    }
</code>
in router
<code>
get("version"){
            request in
            let result = try Pokemon.database?.driver.raw("select sqlite_version();")
            return try JSON(node: result)
        }

</code>

<h2>MySql</h2>
start mysql server
<code>docker run -p 3306:3306 --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest</code>

