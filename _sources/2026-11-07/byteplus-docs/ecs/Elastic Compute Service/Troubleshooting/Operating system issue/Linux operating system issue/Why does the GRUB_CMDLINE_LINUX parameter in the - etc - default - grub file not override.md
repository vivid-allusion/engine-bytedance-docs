---
title: "Why does the GRUB_CMDLINE_LINUX parameter in the /etc/default/grub file not override the kernel command line parameters in all BLS snippets after I execute the grub2-mkconfig command?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/GRUB_CMDLINE_LINUX"
---

<span id=".5Li65LuA5LmI5omn6KGMZ3J1YjItbWtjb25maWflkb3ku6TlkI7vvIzmsqHmnInkvb_nlKgvZXRjL2RlZmF1bHQvZ3J1YuaWh-S7tuS4reeahEdSVUJfQ01ETElORV9MSU5VWOWPguaVsOWAvOimhuebluaJgOaciUJMU-S7o-eggeeJh-auteS4reeahOWGheaguOWRveS7pOihjOWPguaVsO-8nw=="></span>
## **Causes**

This may occur because the value of the `GRUB_ENABLE_BLSCFG` parameter in the /etc/default/grub file of the CentOS operating system has been modified from the default value to `true`, which changes the default behavior of `grub2-mkconfig`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This change is due to an update in the configuration method of the crashkernel parameter by kexec\-tools. Overriding the kernel command line in Boot Loader Specification (BLS) snippets will result in the loss of the crashkernel parameter and failure to start the kdump service. <a href="https://bugzilla.redhat.com/show_bug.cgi?id=2212320">Learn more</a>.</div>


<span id="0Dr4AnbC"></span>
## **Solutions**

* You can add the `--update-bls-cmdline` option when you execute the `grub2-mkconfig` command. The system will update the kernel command line in the BLS snippets according to `GRUB_CMDLINE_LINUX`.

   ```Plain Text
    grub2-mkconfig -o </path/to/grub.cfg> --update-bls-cmdline
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code></path/to/grub.cfg></code> with the actual grub.cfg path.   </div>
   

   * You can also use the `grubby` command to modify the BLS code snippet for the specified kernel.

   ```Plain Text
   grubby --update-kernel </path/to/kernel> --args "<new args>"
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code></path/to/kernel></code> with the actual path to the kernel file. Replace <code><new args></code> with the actual kernel parameters.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you want to modify kernel parameters in the CentOS Stream 9 operating system, we recommend that you use this method.   </div>
