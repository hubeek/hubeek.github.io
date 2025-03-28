# Crash Log Helper

_Status: Published_
_Created: 2017-02-17 03:07:11_
_Tags: objC_

.h
<code>
@interface CrashLogHelper : NSObject

+(void) writeNoCrashFile;
+(void) removeNoCrashFile;
</code>
.m
<code>


+(void) writeNoCrashFile
{
    NSError *error;
    NSString *filePath = [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject] stringByAppendingPathComponent:@"crashloggername.txt"];
    NSLog(@"file path for write nocrash file%@", filePath);
    NSFileManager *filemgr;
    
    filemgr = [NSFileManager defaultManager];
    
    if ([filemgr fileExistsAtPath: filePath ] == YES)
    {
        NSLog (@"File exists, so it did crash"); 
        [App.persistenceHelper setString:@"-1" forPersistentKey:PERSISTENCEHELPER_ratingsequence];
    }
    else
    {
        NSLog (@"File not found");
        // write new file
        NSString *stringToWrite = @"no crash";
        [stringToWrite writeToFile:filePath atomically:YES encoding:NSUTF8StringEncoding error:&error];
    }
}
+(void) removeNoCrashFile
{
    NSFileManager *filemgr;
    NSError *error;
    filemgr = [NSFileManager defaultManager];
    NSString *filePath = [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject] stringByAppendingPathComponent:@"crashlogger.txt"];
   
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