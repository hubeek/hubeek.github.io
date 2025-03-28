# Cocoapods in Playgrounds

_Status: Published_
_Created: 2016-04-04 06:33:36_
_Tags: swift_

Install:

$ gem install cocoapods-playgrounds
Create a Playground with Alamofire:

$ pod playgrounds Alamofire
Create a Playground with multiple pods:

$ pod playgrounds RxSwift,RxCocoa
The new Playground will automatically open.

You will have to first build the project, to enable the pods, then the Playground will be available.

===
Or:


During the app development, you may find a third-party libraries or frameworks may save you a lot of time and let you focus on your fancy features. However, you always want to verify whether the functions provided by the library are what you expect. To do so, playground is a prefect place to test them out.

Using CocoaPods
CocoaPods manages library dependencies for your Xcode projects. 
You first need to install CocoaPods. Open Terminal and enter the following command:

 sudo gem install cocoapods  

Enter your password when requested. Then enter this command in Terminal to complete the setup:

 pod setup --verbose  

This process will likely take a few minutes, and the verbose option logs progress as the process runs, allowing you to watch the process instead of seeing a seemingly â€œfrozenâ€ screen.

Installing Your Dependency
Create a Xcode project if you don't have one, and then close Xcode.
Open Terminal and navigate to the directory that contains your project:

 cd ~/Path/To/Folder/Containing/YourProject  

Next, enter this command:

 pod init  

This creates a Podfile for your project.
Open the Podfile using Xcode for editing, and you can use this command:

 open -a Xcode Podfile  

The default Podfile looks like this:

 # Uncomment this line to define a global platform for your project  
 # platform :ios, '8.0'  
    
 target 'YourProject' do  
    
 end  
    
 target 'YourProjectTests' do  
    
 end  

Change it with following:

 platform :ios, "8.0"  
 use_frameworks!  
   
 link_with 'YourProject', 'YourProjectTests'  
 pod 'Alamofire'  
 pod 'SwiftyJSON'  

In my example, I am going to use Alamfire and SwiftyJSON libraries in my project. You can change it to whatever library you would like to play with.

Jump back the Terminal, and use this command to install pods:

 pod install  

And after the installation, the last line of the output should be like this:

 [!] Please close any current Xcode sessions and use `YourProject.xcworkspace` for this project from now on.  

The CocoaPads creates a workspace based on your project, as the command-line warning mentioned, you must always use the workspace and not the project, otherwise youâ€™ll encounter build errors.

By using a workspace, all dependencies are available cross the workspace.
Create a playground in the workspace,  and add it to the Podfile with following:

 platform :ios, "8.0"  
 use_frameworks!  
   
 link_with 'YourProject', 'YourProjectTests', 'YourPlayground'  
 pod 'Alamofire'  
 pod 'SwiftyJSON'  

You can import  and use the pod your have installed in the playground:

 //: Playground - noun: a place where people can play  
   
 import UIKit  
   
 var str = "Hello, playground"  
   
 import SwiftyJSON  
 import Alamofire  

Congratulations, you can play with your third-party pods in Playground!