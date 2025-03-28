# emitter explosion

_Status: Published_
_Created: 2018-02-22 15:30:54_
_Tags: iOS swift_

<code>

import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
         createParticles()
    }

    func createParticles() {
        let v = UIView(frame: CGRect(x: 180, y: 220, width: 60, height: 60))
        //v.backgroundColor = .lightGray
        view.addSubview(v)
        let particleEmitter = CAEmitterLayer()
        
        particleEmitter.emitterPosition = CGPoint(x: 30, y: 30)
        particleEmitter.emitterShape = kCAEmitterLayerSphere
        particleEmitter.emitterSize = CGSize(width: 1, height: 1)
        
        let red = makeEmitterCell(color: UIColor.red)
        let green = makeEmitterCell(color: UIColor.green)
        let blue = makeEmitterCell(color: UIColor.blue)
        
        particleEmitter.emitterCells = [red, green, blue]
        
        v.layer.addSublayer(particleEmitter)
        UIView.animate(withDuration: 2.0, animations: {
            v.alpha = 0
        }) { (_) in
            v.layer.sublayers?.removeAll()
        }
    }
    
    func makeEmitterCell(color: UIColor) -> CAEmitterCell {
        let cell = CAEmitterCell()
        cell.birthRate = 2.5
        cell.lifetime = 1.9
        cell.lifetimeRange = 1
        cell.color = color.cgColor
        cell.velocity = 158
        cell.velocityRange = 45
        cell.emissionLongitude = CGFloat.pi
        cell.emissionRange = CGFloat.pi
        cell.spin = 4
        cell.spinRange = 6
        cell.scaleRange = 0.04
        cell.scaleSpeed = 0.3
        cell.xAcceleration = -0.03
        cell.yAcceleration = -0.05
        cell.zAcceleration = 0.2
        
        cell.contents = UIImage(named: "cp")?.cgImage
        return cell
    }
}

</code>