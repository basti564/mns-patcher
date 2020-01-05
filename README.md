# mns-patcher
## Intro
This is a standalone POC using the main exploit used in [MNSPlusTrasher](https://github.com/basti564/MNSPlusTrasher)
## Theory
The theory behind this exploid is that the packages send to the "mnsscreengrabber" service on the student pc are never validated or blocked.
## First Approaches
We could abuse this by either by writing our own remote (which whould require extensive reverse engineering) or patching this test in the frmMain class of the mainForm.cs file in the TeacherConsole executable.

![main](https://user-images.githubusercontent.com/34898868/71782764-28160b80-2fde-11ea-82be-56227af35931.PNG)

The problem with this aproach is that we need to get ahold of the 15 year old [Visual Studio 2005](https://www.microsoft.com/de-de/download/details.aspx?id=804) that has been used to originally compile TeacherConstole and [Janus](http://www.janusys.com) which has also been used in this project
## Final POC
The final POC patches the isTeacher function of all users in dynamic link dibrary "RoomMgr.dll", which is able to compile in newer Visual Studio versions and easily modifyed to our needs.
We only need to modify the return value to "true".

![isTeacher](https://user-images.githubusercontent.com/34898868/71782877-6bbd4500-2fdf-11ea-8a6e-fb5932008b2a.PNG)
## Optionally
You can try to control teacher computers by removing the isTeacherComputer check, which probably won't work as teacher computers don't start the ScreenGrabber service, which is needed to control them. (But you can at least try)

![isTeacherComputer](https://user-images.githubusercontent.com/34898868/71782876-6bbd4500-2fdf-11ea-992b-c378ee6be3cf.PNG)
