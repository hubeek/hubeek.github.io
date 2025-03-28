# find in array times, Slow in build functionality...

_Status: Published_
_Created: 2016-02-19 03:40:05_
_Tags: swift_

Consider this
<code>
func getCell(x:Int, y:Int) -> GameBoardCell?{
    let start1 = NSDate()
    if let r = gameBoardCells.indexOf({$0.xPos == x && $0.yPos == y})
    {
      let end1 = NSDate()
      let timeInterval: Double = end1.timeIntervalSinceDate(start1)
      print("Time to evaluate problem1: \(timeInterval)")
      //return gameBoardCells[i]
    }
    
    
    let start2 = NSDate()
    let result = gameBoardCells.filter ({$0.xPos == x && $0.yPos == y})
    if result.count > 0
    {
      let end2 = NSDate()
      let timeInterval2: Double = end2.timeIntervalSinceDate(start2)
      print("Time to evaluate problem2: \(timeInterval2) count \(result.count)")
      
      //return result.first
    }
    
    
    let start3 = NSDate()
    for c in gameBoardCells
    {
      if(c.xPos == x && c.yPos == y)
      {
        let end3 = NSDate()
        let timeInterval3: Double = end3.timeIntervalSinceDate(start3)
        print("Time to evaluate problem3: \(timeInterval3)")
        return c
      }
    }
    return nil
  }
</code>

in the beginning with small array
Time to evaluate problem1: 0.000268995761871338
Time to evaluate problem2: 0.000285029411315918 count 1
Time to evaluate problem3: 0.000150978565216064

results with large array
Time to evaluate problem1: 3.80277633666992e-05
Time to evaluate problem2: 0.000289022922515869 count 1
Time to evaluate problem3: 2.3961067199707e-05

So Old school looping is quicker than using the build in functionality
