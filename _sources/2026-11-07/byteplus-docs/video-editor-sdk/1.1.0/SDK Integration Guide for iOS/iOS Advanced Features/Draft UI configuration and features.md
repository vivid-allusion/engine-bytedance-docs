---
title: "Draft UI configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-draft-ui-configuration-and-features_1_1_0"
---

Draft UI configuration encompasses the layout and functionality settings tailored for the draft screen within an application. This configuration allows users to organize, edit, and manage drafts efficiently, ensuring a seamless drafting experience.

```objectivec
@protocol EODraftBoxControllerDelegate <NSObject>
@optional
- (void)draftBoxControllerDidCancel:(EODraftBoxController *)draftBoxController;
- (void)draftBoxController:(EODraftBoxController *)draftBoxController didSelectDraft:(EOSDKDraftModel *)draftModel;
@end

@interface EODraftBoxController : UIViewController

@property (nonatomic, weak) id<EODraftBoxControllerDelegate> delegate;

+ (void)presentDraftVCDelegate:(id<EODraftBoxControllerDelegate>)delegate;

 //  The presentVC is used as the basis for presentation. It needs to be the topmost view controller. 
 
+ (void)presentDraftVCDelegate:(id<EODraftBoxControllerDelegate>)delegate presentVC:(UIViewController *)presentVC;

@end
```


<span id="69caa0be"></span>
# Example: Implementing a delegate

```Swift
extension EffectOneModule: EODraftBoxControllerDelegate {
    func draftBoxController(_ draftBoxController: EODraftBoxController, didSelectDraft draftModel: EOSDKDraftModel) {
        self.showEditorViewController(.draft(draftModel), presenter: draftBoxController)
    }
}
```


<span id="fdcc5a56"></span>
# **Code sample**

```Swift
//  The first method.
EODraftBoxController.presentDraftVCDelegate(self)
//The second method.
EODraftBoxController.presentDraftVCDelegate(self, presentVC: viewController)
```
