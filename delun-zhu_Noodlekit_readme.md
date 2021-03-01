NoodleKit
=========

This is a random collection of classes and categories that I am making public. Most of this code has been posted on my blog:  

The project is primarily structured to build a framework. There are targets for various examples showing how the different classes are used. Some of the examples also contain a Read Me file so check those out for more details on the specific classes.

This framework is meant to be built/used on 10.6 and later and should support 64-bit.

This code is maintained at   . Please post any issues and requests there.

What nifty stuff is in here?
----------------------------

#### NSObject-NoodlePerformWhenIdle  
NSObject category for calling a method when the user has been idle for the specified amount of time. Useful for putting up non-critical alerts and purging memory caches, among other things.  
 

#### NSIndexSet-NoodleExtensions
Provides an enumerator to cycle through the indexes in an NSIndexSet. Not featured directly in any blog article but used for the "Row Spanning Columns" feature (see below).

#### NSTimer-NoodleExtensions
Allows you to create timers that treat the fire date as absolute. Normally, NSTimer will adjust the time if you put the machine to sleep. This category makes it such that it will fire on the date you told it to originally. 
 

#### NoodleGlue
Little class that allows you to plug a block into some code that requires a target/selector. Check the NSTimer category too see how it can be used.
 

#### NSObject-NoodleCleanupGlue
A category on NSObject that allows you to add a block that will be executed when the object is deallocated. It is based on NoodleGlue and it is lumped into the same source file with it.
 

#### NSResponder-NoodleModalExtensions  
NSResponder category providing methods that will dismiss a dialog and return the proper code for whatever button (OK/Cancel) was clicked. Just hook your dialog buttons up to these methods in IB and you're set. Alleviates having to write that glue code every time.  
 

#### NSImage-NoodleExtensions  
NSImage category providing methods to draw NSImages with correct orientation and scaling regardless of the flipped status of the image or the context being drawn into.  
 

#### NoodleCustomImageRep
NSImageRep subclass that allows you to specify the drawing via a block. Handy for drawing images without having to create a new subclass of NSImageRep.
 

#### NSWindow-NoodleEffects  
Provides a basic zoom effect for NSWindow.  
   
 

#### NoodleLineNumberView, NoodleLineNumberMarker  
Adds line numbers (and corresponding markers) to NSTextView.  
 

#### NSTableView-NoodleExtensions, NoodleTableView, NoodleIPhoneTableView
The NSTableView category and NoodleTableView are a consolidation of the sticky row header tableview
and row spanning tableview featured on my blog.

#####Sticky Row Headers
An NSTableView category that does sticky row headers, like with UITableView on the iPhone. NoodleTableView implements the basic hooks to enable the feature while NoodleIPhoneTableView simulates the look and feel of UITableView.
 

#####Row Spanning Columns
Certain columns can be made to allow their cells to span across multiple rows. These spans are determined by contiguous sections of rows with the same object value. You can enable this in NoodleTableView by using NoodleTableColumns for any columns you want to exhibit this behavior. Remember to enable the property on each column or call -setRowSpanningEnabledForCapableColumns: to enable it for all NoodleTableColumns in the tableview.
 


License
-------

Copyright (c) 2007-2012 Noodlesoft, LLC. All Rights Reserved.

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)