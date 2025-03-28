# Write/Read data to .plist file

_Status: Published_
_Created: 2015-01-25 14:59:42_
_Tags: objC_

First of all add a plist to your project in Xcode. For example â€œdata.plistâ€.
<code>
NSError *error;
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES); //1
NSString *documentsDirectory = [paths objectAtIndex:0]; //2
NSString *path = [documentsDirectory stringByAppendingPathComponent:@â€data.plistâ€]; //3

NSFileManager *fileManager = [NSFileManager defaultManager];

if (![fileManager fileExistsAtPath: path]) //4
{
NSString *bundle = [[NSBundle mainBundle] pathForResource:@â€dataâ€ ofType:@â€plistâ€]; //5

[fileManager copyItemAtPath:bundle toPath: path error:&error]; //6
}
</code>
1) Create a list of paths.
2) Get a path to your documents directory from the list.
3) Create a full file path.
4) Check if file exists.
5) Get a path to your plist created before in bundle directory (by Xcode).
6) Copy this plist to your documents directory.
next read data:
<code>
NSMutableDictionary *savedStock = [[NSMutableDictionary alloc] initWithContentsOfFile: path];

//load from savedStock example int value
int value;
value = [[savedStock objectForKey:@â€valueâ€] intValue];

[savedStock release];
</code>
write data:
<code>
NSMutableDictionary *data = [[NSMutableDictionary alloc] initWithContentsOfFile: path];

//here add elements to data file and write data to file
int value = 5;

[data setObject:[NSNumber numberWithInt:value] forKey:@â€valueâ€];

[data writeToFile: path atomically:YES];
[data release]
</code>

1) You must create a plist file in your Xcode project.
2) To optimize your app, better is to save all the data when application (or for example view) is closing. For instance in applicationWillTerminate. But if you are storing reeaaaally big data, sometimes it couldnâ€™t be saved in this method, becouse the app is closing too long and the system will terminate it immediately.