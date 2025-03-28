# fetch find Core Data

_Status: Published_
_Created: 2015-04-08 03:42:33_
_Tags: swift_

<code>
    let appDel = UIApplication.sharedApplication().delegate as AppDelegate
    let fetchRequest = NSFetchRequest(entityName: "Puzzle")
    let predicate = NSPredicate(format: "title == %@", "Best Language")
    fetchRequest.predicate = predicate
    let managedContext = appDel.managedObjectContext
    var error:NSError?
    // Execute the fetch request, and cast the results to an array of LogItem objects
    if let fetchResults = managedContext?.executeFetchRequest(fetchRequest, error: &error){
      if error != nil {
        println("error fetch request \(__FUNCTION__)")
        
      }else {
        
        println("num results \(fetchResults.count)")
        
        
      }
</code>