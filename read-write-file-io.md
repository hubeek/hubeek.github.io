# Read Write file IO 

_Status: Published_
_Created: 2017-02-08 04:39:07_
_Tags: objC_

<code>
+(void) writeTextFile
{
    NSError *error;
    NSString *filePath = [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject] stringByAppendingPathComponent:@"text.txt"];
    NSFileManager *filemgr;
    
    filemgr = [NSFileManager defaultManager];
    
    if ([filemgr fileExistsAtPath: filePath ] == YES)
    {
        NSLog (@"File exists"); 
    }
    else
    {
        NSLog (@"File not found");
        // write new file
        NSString *stringToWrite = @"text text text";
        [stringToWrite writeToFile:filePath atomically:YES encoding:NSUTF8StringEncoding error:&error];
    }
}
+(void) removeTextFile
{
    NSFileManager *filemgr;
    NSError *error;
    filemgr = [NSFileManager defaultManager];
    NSString *filePath = [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject] stringByAppendingPathComponent:@"text.txt"];
   
    if ([filemgr fileExistsAtPath: filePath ] == YES){
        NSLog (@"File exists so remove");
        BOOL success = [filemgr removeItemAtPath:filePath error:&error];
        if (success) {
            NSLog(@"file removed");
        }
        else
        {
            NSLog(@"Could not delete file -:%@ ",[error localizedDescription]);
        }
    }
    else{
        NSLog (@"File not found"); // something fishy
    }
    
}
</code>