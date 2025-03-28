# Blurred footprint

_Status: Published_
_Created: 2017-12-06 02:48:50_
_Tags: iOS swift_

extension uiimage
<code>
public func modifiedImage(_ draw: (CGContext, CGRect) -> ()) -> UIImage {
        
        // using scale correctly preserves retina images
        UIGraphicsBeginImageContextWithOptions(size, false, scale)
        let context: CGContext! = UIGraphicsGetCurrentContext()
        assert(context != nil)
        
        // correctly rotate image
        context.translateBy(x: 0, y: size.height)
        context.scaleBy(x: 1.0, y: -1.0)
        
        let rect = CGRect(x: 0.0, y: 0.0, width: size.width, height: size.height)
        
        draw(context, rect)
        
        let image = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        return image!
    }
public func tintPictogram(with fillColor: UIColor) -> UIImage {
        
        return modifiedImage { context, rect in
            // draw tint color
            context.setBlendMode(.normal)
            fillColor.setFill()
            context.fill(rect)
            
            // mask by alpha values of original image
            context.setBlendMode(.destinationIn)
            context.setAlpha(0.15)
            context.draw(cgImage!, in: rect)
        }
    }

</code>
general:
<code>
func blurImage(_ image:UIImage) -> UIImage? {
    let context = CIContext(options: nil)
    let inputImage = CIImage(image: image)
    let originalOrientation = image.imageOrientation
    let originalScale = image.scale
    
    let filter = CIFilter(name: "CIGaussianBlur")
    filter?.setValue(inputImage, forKey: kCIInputImageKey)
    filter?.setValue(3.0, forKey: kCIInputRadiusKey)
    let outputImage = filter?.outputImage
    
    var cgImage:CGImage?
    
    if let asd = outputImage
    {
        cgImage = context.createCGImage(asd, from: (inputImage?.extent)!)
    }
    
    if let cgImageA = cgImage
    {
        return UIImage(cgImage: cgImageA, scale: originalScale, orientation: originalOrientation)
    }
    
    return nil
}
</code>
use:
<code>
if let image = UIImage(named:name)
            {
                 let tintimg = image.tintPictogram(with: .black)
                if let shadowedimage = blurImage(tintimg){
                //...    shadowImages.append(shadowedimage)
                }
                
            }
</code>