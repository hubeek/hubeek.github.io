# static var in Objc replaced by statemachinetype in swift

_Status: Published_
_Created: 2015-02-20 16:15:05_
_Tags: swift_

<code>
typealias StateMachineType = ()->Int

func makeStateMachine(maxState:Int)->StateMachineType{
  
  var currentState:Int = 0
  return {
    currentState++
    if currentState > maxState{
      currentState = 0
    }
    return currentState
  }
}
</code>