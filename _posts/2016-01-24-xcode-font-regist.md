---
layout: post
title:  "Xcode, custom font not register"
date:   2016-01-24 02:00:00 +0900
categories: Exceptions
---
#1.Regist Custom font, 2 ways
- info.plist -> add font name to [Fonts provided by application] category
- use below code

~~~c++
void registFont(const string& file_name)
{
    // get ttf file path
    NSString* basePath = [NSString stringWithUTF8String:file_name.c_str()];
    NSString* resourcePath = [[NSBundle mainBundle] resourcePath];
    NSString* fullPath = [resourcePath stringByAppendingPathComponent:basePath];

    // regist the font
    CGDataProviderRef fontDataProvider = CGDataProviderCreateWithFilename([fullPath UTF8String]);
    CGFontRef customFont = CGFontCreateWithDataProvider(fontDataProvider);
    CGDataProviderRelease(fontDataProvider);
    CFErrorRef error;
    if (! CTFontManagerRegisterGraphicsFont(customFont, &error)) {

    CFStringRef errorDescription = CFErrorCopyDescription(error);
    NSLog(@"Failed to load font %s: %@", file_name.c_str(), errorDescription);
    CFRelease(errorDescription);
    }
    else
    Log::info_print("registFont %s success", file_name.c_str());

    CGFontRelease(customFont);
}
~~~


#3.Xcode Bug
- Sometimes a font is not registed, although you follow above step. At this times, remove  the font’s reference, and then add the reference again.