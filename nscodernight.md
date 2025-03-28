# nscodernight

_Status: Published_
_Created: 2016-06-29 09:52:29_
_Tags: swift_

<code>
let containerView = UIView(frame: CGRect(x: 0.0, y: 0.0, width: 375.0, height: 667.0))
XCPlaygroundPage.currentPage.liveView = containerView
containerView.backgroundColor = #colorLiteral(red: 0, green: 0, blue: 0, alpha: 1)

var view = UIView()
view.frame = CGRect(x: 0, y: 0, width: 300, height: 200)
view.backgroundColor = #colorLiteral(red: 0.9346159697, green: 0.6284804344, blue: 0.1077284366, alpha: 1)
containerView.addSubview(view)

let timing = UICubicTimingParameters(animationCurve: .easeIn)

let animator = UIViewPropertyAnimator(duration: 5.0, timingParameters: timing)
animator.addAnimations
  {
    view.center = containerView.center
}



let scene = UIViewPropertyAnimator(duration: 2.0, timingParameters: timing)
scene.addAnimations { 
  containerView.backgroundColor = #colorLiteral(red: 0.2818343937, green: 0.5693024397, blue: 0.1281824261, alpha: 1)
}
scene.addCompletion { (_) in
  view.backgroundColor = #colorLiteral(red: 0.1991284192, green: 0.6028449535, blue: 0.9592232704, alpha: 1)
}
animator.addCompletion
  { _ in
      scene.startAnimation()
    
}
animator.startAnimation()

</code>