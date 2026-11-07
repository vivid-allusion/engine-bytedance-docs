---
title: "Draft UI configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-draft-ui-configuration-and-features"
---

Draft UI configuration encompasses the layout and functionality settings tailored for the draft screen within an application. This configuration allows users to organize, edit, and manage drafts efficiently, ensuring a seamless drafting experience

```objectivec
#import <UIKit/UIKit.h>
NS_ASSUME_NONNULL_BEGIN

@protocol EOVideoEditorViewControllerDelegate;
@interface EODraftBoxController : UIViewController

//delegate: Create a delegate to set up a callback for the preview editor page.
+ (void)presentDraftVCDelegate:(id<EOVideoEditorViewControllerDelegate>)delegate;

// delegate: Create a delegate to set up a callback for the preview editor page.
//presentVC: Presents a controller-based view. The presentVC parameter need to be set as a top VC.
+ (void)presentDraftVCDelegate:(id<EOVideoEditorViewControllerDelegate>)delegate presentVC:(UIViewController *)presentVC;

@end

NS_ASSUME_NONNULL_END
```


<span id="fdcc5a56"></span>
# **Code sample**

```Swift
// The first method.
EODraftBoxController.presentDraftVCDelegate(self)
//The second method.
EODraftBoxController.presentDraftVCDelegate(self, presentVC: viewController)
```
