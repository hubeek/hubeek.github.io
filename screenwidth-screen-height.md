# Screenwidth screen height

_Status: Published_
_Created: 2017-02-08 04:41:34_
_Tags: objC_

<code>
+ (CGFloat) getScreenWidth
{
    CGFloat swidth = [UIScreen mainScreen].bounds.size.width;
    CGFloat sheight = [UIScreen mainScreen].bounds.size.height;
    return MIN(swidth, sheight);
}

+ (CGFloat) getScreenHeight
{
    CGFloat swidth = [UIScreen mainScreen].bounds.size.width;
    CGFloat sheight = [UIScreen mainScreen].bounds.size.height;
    return MAX(swidth, sheight);
}
</code>