# MT5 iPhone development build

This fork uses UTM's iOS QEMU engine for an iPhone 11 running iOS 26 or later.
The GitHub Actions workflow produces `MT5-iOS-Emulator.ipa` for development signing.
The UTM interface, license, and third-party credits are retained.

## Install and run

1. Download the unsigned IPA artifact from a successful **Build iPhone IPA** run.
2. Sign it with a development certificate using AltStore, SideStore, or an
   equivalent development signing tool. A free account needs renewal every seven
   days. The embedded iOS helper extension also needs development signing.
3. Enable JIT with a compatible debugger/JIT enabler for your iOS release.
4. Import or create a guest VM, supply its operating-system image, and install
   Exness MT5 inside the guest. Guest images add download and storage requirements.
5. Enable **Continue running VM in the background** in the app's settings, then
   start or resume the VM while the app is in the foreground.

## Background behavior

On iOS 26, the app requests a user-started continued-processing task when the VM
starts. The system displays its progress in a Live Activity. Each session has a
24-hour budget. Stopping or pausing the VM completes the task. At the budget limit
or on system expiration, the app requests a VM pause and reports that the session
ended. Return to the app and resume to request another session.

Resource pressure, task cancellation, signing expiry, and JIT availability can
interrupt execution. On-device validation of this build, MT5 performance, and
background behavior on the iPhone 11 is pending.

## Build provenance

Native dependencies come from UTM's `Sysroot-ios-arm64` artifact in Actions run
`41750855227`, built from commit `c862bc145387000c4451fc6a654133f8784c3df7`.
Dependency scripts and patches match the source baseline used by this fork.

References

- [UTM iOS development](iOSDevelopment.md)
- [UTM iOS installation and JIT](https://docs.getutm.app/installation/ios/)
- [Apple continued-processing tasks](https://developer.apple.com/documentation/BackgroundTasks/performing-long-running-tasks-on-ios-and-ipados)
