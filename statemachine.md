# stateMachine

_Status: Published_
_Created: 2015-03-11 15:27:01_
_Tags: swift_

<h2>as global func/type </h2>
<code>
typealias StateMachineType = () -> Int

func makeStateMachine(maxState:Int) -> StateMachineType{
  var currrentState: Int = 0
  
  return {
    
    currrentState++
    if currrentState > maxState {
      currrentState = 0
    }
    return currrentState
  }
  
}
</code>