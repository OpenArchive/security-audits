At OpenArchive, we strive to make our Save app as safe as possible. Through support from the Open Tech Fund's (OTF) Red Team Lab, we successfully completed a third-party security audit conducted by Trail of Bits. Please find the [OTF report here](https://www.opentech.fund/results/security-safety-audits/openarchive-save-android-ios/) and the Trail of Bits report here. We are pleased with the results and hope our stakeholders can take comfort in knowing our tool is secure. 

Outcomes: Our tech team was able to resolve all security vulnerabilities identified in the audit. However, due to architectural constraints and third-party dependencies, we were only able to partially resolve some issues. Below, we map our plan to address outstanding issues. 

# Save iOS

Trail of Bits finished their initial audit of the iOS version of the Save app in Winter of 2023 and then reviewed the fixes and mitigations implemented by the OpenArchive team to resolve the issues identified in their initial audit report. 

OpenArchive’s team addressed and solved most of the issues identified by Trail of Bits, partially resolved one minor issue which depends on the DropBox API (ID 2) and did not resolve one minor issue (ID 5).

The one unresolved issue (ID 5) involves disguising the app icon when Save is moved to the background. We are currently planning to implement different options to hide the use of Save in the future. For example, some apps call this function a discrete or disguised app setting and allow the user to change the main app icon and its screen while in the background to a calculator, a to-do list, or something else.  

# Save Android

Trail of Bits finished their initial audit of the Android version of the Save app this Spring 2023 and then reviewed the fixes and mitigations implemented by the OpenArchive team to resolve the issues identified in their initial audit report. We have addressed and solved most of the issues identified by Trail of Bits.
There are some issues that are either partially resolved or not resolved yet. These issues either do not represent a threat to Save users, are not directly exploitable, or are dependent on third-party libraries that we use.
OpenArchive’s team addressed and solved most of the issues identified by Trail of Bits. There are some issues that are either partially resolved or not resolved yet. These issues either do not represent a threat to Save users, are not directly exploitable, or are dependent on third-party libraries that we use.

(ID 2) Save uses a deprecated LocalBroadcastManager class, which wasn’t updated because  there's nothing about the use of this class that's exploitable or that would disrupt the app's functionality. We will consider updating this in the future while improving the overall code quality of the app.

(ID 13) Save had a path traversal vulnerability. This was fixed, but we still allow the content uri to use the format ”content://” instead of just “file://”.​​ We did this so that our users could upload their chosen files to their backend and don’t want to restrict app functionality or sharing between other apps and Save.

Save use libproofmode to digitally sign media files (ID 4, 19). We were originally using a static password to encrypt the private key used by libproofmode. We are now encrypting the PGP private key used by libproofmode with the user's password. We are aware this solution is not optimal, but at the same time it provides, what we believe, was the right balance between usability and data security.
Libproofmode has also only recently started using a different key management system (ID 19). Save still implements only PGP at the moment, and we are currently evaluating how we can improve this in the future. 

Save does not warn users about using EXIF data in media files (ID 15). We believe EXIF data is crucial to authenticate evidentiary media and that users are aware that this is part of the app functionality through our guides and trainings. We will also include the risks of EXIF data attached to media files in our documentation. 

(ID 17) While we intensely QA our app, we do not yet implement automated testing. We have just started using a testing platform to test our app on various devices and network conditions, but this will take some time to be fully implemented in a CI pipeline.
