# Audio in ViewController

_Status: Published_
_Created: 2015-07-31 09:37:24_
_Tags: swift_

<code>
import Foundation
import AVFoundation
import UIKit

class AudioPlayerHelper {
  
  static func setupAudioPlayerWithFile(file: String, type:String)-> AVAudioPlayer?
  {
    
    let path = NSBundle.mainBundle().pathForResource(file as String, ofType: type as String)
    let url = NSURL.fileURLWithPath(path!)
    do{
      let audioplayer = try AVAudioPlayer(contentsOfURL: url)
      return audioplayer
    }
    catch{
      return nil
    }
   
    
  }
}
</code>

<code>
import UIKit
import AVFoundation

class ViewController: UIViewController {

  var click = AVAudioPlayer()
  var whistle = AVAudioPlayer()
  
  override func viewDidLoad() {
    super.viewDidLoad()
   
    whistle = AudioPlayerHelper.setupAudioPlayerWithFile("whistle", type: "wav")
    click = AudioPlayerHelper.setupAudioPlayerWithFile("click", type: "wav")
    
  }

  @IBAction func clickpressed(sender: UIButton) {
    click.play()
  }

  @IBAction func whistlePressed(sender: UIButton) {
    whistle.play()
  }
}
</code>
in swift 4
<code>
import AVFoundation
class ViewController: UIViewController {

    var buttonSoundEffect: AVAudioPlayer?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let path = Bundle.main.path(forResource: "button.mp3", ofType:nil)!
        let url = URL(fileURLWithPath: path)
        
        do {
            buttonSoundEffect = try AVAudioPlayer(contentsOf: url)
            buttonSoundEffect?.prepareToPlay()
        } catch {
            // couldn't load file :(
        }
    }

    @IBAction func buttonpressed(_ sender: UIButton) {
        
        buttonSoundEffect?.play()
    }
    
}</code>