# uiiamge background

_Status: Published_
_Created: 2014-06-11 09:52:20_
_Tags: objC_

UIGraphicsBeginImageContext(self.view.frame.size);
    [[UIImage imageNamed:@"statistics"] drawInRect:self.view.bounds];
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    UIImageView *imageView = [[UIImageView alloc] initWithImage: image];
    
    [self.view addSubview: imageView];
    
    [self.view sendSubviewToBack: imageView];