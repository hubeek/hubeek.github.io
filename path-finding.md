# Path Finding 

_Status: Published_
_Created: 2017-09-21 04:09:32_
_Tags: swift_

<code>
import GameplayKit

let graph = GKGraph()


let nodeA = GKGraphNode()
let nodeB = GKGraphNode()
let nodeC = GKGraphNode()
let nodeD = GKGraphNode()
let nodeE = GKGraphNode()


graph.addNodes([nodeA,nodeB,nodeC,nodeD,nodeE])
nodeA.addConnectionsToNodes([nodeB,nodeD], bidirectional: true)
nodeB.addConnectionsToNodes( [nodeD], bidirectional: true)
nodeC.addConnectionsToNodes( [nodeE], bidirectional: false)
nodeD.addConnectionsToNodes( [nodeC], bidirectional: false)
let path:[GKGraphNode] = graph.findPathFromNode(nodeA, toNode: nodeE)

</code>