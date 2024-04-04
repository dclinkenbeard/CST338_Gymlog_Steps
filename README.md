# GymLog Application
All of the associated videos are linked [in this Panopto folder](https://csumb.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx?folderID=d53a137e-e309-4177-a3ee-b0c001711ca0). It may be necessary to log in to your CSUMB account to view the videos.
The goal of this project is to work through all the steps necessary to create an app that uses the Room database wrapper for persistence and that allows users to log in. 
If I am feeling brave I will add in a recycler view too.

## Overview and plan
**NO VIDEO YET** 
This is the overall view of the final product.  Once I get the login screen setup and working, including the logout features, I will record this video.  Anything afer this (editing logs, more user info, etc. Will be shown in their respective video).


## Video 01: Setup
1. Create a gitignore file
2. Create a branch
3. make the initial layout

## Video 02: Basic functions
1. Add [viewBindings](https://developer.android.com/topic/libraries/view-binding) 
1. Wire up the button
1. Read information from the display
1. Log our info
1. Test the display

## Video 03: Add the Database
1. Add the room dependancies
   * [Android Room Dependency](https://developer.android.com/jetpack/androidx/releases/room)
1. create the POJO entity objects
	* for now just a GymLog
1. Create the database interface
1. Create the GymLog DAO
1. Make the repository
	* Requires lots of lambdas and auto-completes

## Video 04: Use the Database
1. Create a type converter
1. Use the Room Repo to write/read logs.

## Video 05: fix the problems
1. Add a singleton to fix the non main thread issue
1. Show the app inspector
1. Write a log to the DB
1. show it in app inspector!
1. add a toString

## Video 06: Update display
1. Fix it so an empty string will not insert a log
1. Clean up the toString()
1. Use the retrieved records to update the display.

## Video 07: Add users
1. Create a User POJO
1. User DAO
1. Update the DB repo to allow user operations
1. Update gymLog to have a userId field

## Video 08: add a login screen
1. Why aren't we getting default users.
	* i.e. why is the callback not working?
1. Add a login screen

## Video 09: add menu and logout function.
1. Add a menu to facilitate logging in and out
	* [Menu resources](https://developer.android.com/guide/topics/resources/menu-resource)
1. Add logout function
1. Add alertDialog for logout.

## Video 10: update our login screen
1. Make login screen use database

## Video 11: Update login screen to use LiveData
1. UserDao --> return LiveData
1. GymLogRepository --> return LiveData
1. update Login method

## Video 12:
1. Add user preferences to store login info
1. Make MainActivity sort by user

## Video 13: ???

## Video 14: Fixing the sharedPreference
[Android Developer documentation on SharedPreference](https://developer.android.com/training/data-storage/shared-preferences#java)
1. Create a method to store userId in the shared preference
1. Update our shared preference to read from the strings.xml file
1. Update logout method
1. Update login method


## Bugs to fix
1. FIXED ~~User login is not persisting... why?~~
1. display is not updating immediatly...
	* Issue is with asynch so adding a recycler will fix it...

## Add a recycler
[Following Android Room With a View guide](https://developer.android.com/codelabs/android-room-with-a-view#0)
1. Update the GymLog DAO to return liveData
	* Done
2. Create the viewHolder
3. Create the adapter
4. Update MainActivity to have a recycler view
5. The fix for the display was:
	1. The problem was that the content needed to 'wrap' in the recylcer item AND the recycler object needed a defined height. So the following changes fixed everything.
	1. gymlog_recycler_item.xml:4
		* change kayout_height to "wrap_content"
	1. activity_main.xml:14
		* change layout_height to 300dp
	1. MainActivity.java:insertGymLogRecord()
		* repository.insertGymLog(log) --> gymLogViewModel.insert(log)

