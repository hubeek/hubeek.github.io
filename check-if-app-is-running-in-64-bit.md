# check if app is running in 64 bit

_Status: Published_
_Created: 2014-11-26 08:58:59_
_Tags: objC_

There are two ways to determine this: at runtime (i.e. in your running code), and at compile time (i.e. before the code is compiled). Letâ€™s take a look at both options.

Runtime Check
// testing for 64bit at runtime
    
    if (sizeof(void*) == 4) {
        self.textLabel.text = @"You're running in 32 bit";
        
    } else if (sizeof(void*) == 8) {
        self.textLabel.text = @"You're running in 64 bit";
    }
Determines the size of a pointer.

Compile Time Check
#if __LP64__
    // you're running 64bit
#else
    // you're running 32bit
#endif
Asks the compiler which architecture it compiles for.