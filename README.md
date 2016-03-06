FSWD - Project 4 - Conference orginization app
Brian Harlin
3/5/16

===============================================
ABSTRACT
===============================================
This is a website for the purpose of allowing people to create conferences, create sessions
for those conferences, view conferences and register for conferences.


================================================
INSTRUCTIONS
================================================
Clone or download repo from https://github.com/rumblefish2494/FSWD-P4 to view and test /
add to on local host or visit live version at https://myapp2494.appspot.com/ to test current
revision through front end and https://myapp2494.appspot.com/_ah/api/explorer for backend testing of endpoints.

app has 23 endpoints APIs as follows:
--------------------------
PROFILE APIs
--------------------------
getProfile:
returns the current user's profile if exists.
errors if does not.

saveProfile:
for updating user profile and saving to google datastore

--------------------------
CONFERENCE APIs
--------------------------

crateConference:
allows user to create a new conference with a name (required),
description, topics, city, startDate format (yyyy-mm-dd), endDate format (yyyy-mm-dd), maxAttendees,
seatsAvailable, and featuredSpeaker(assigned by push task not directly by user).
saves conference to Google Datastore

updateConference:
allows user to make changes to conference fields and save to datastore.

getConference:
requires a conference Key returns conference information.

getConferencesCreated:
returns all conferences created (all fields) by the user requesting.

queryConferences:
returns conferences (all fields) filtered by user entered parameters.

getFeaturedSpeaker: (PROJECT TASK 6 PART 2)
requires a conference Key returns the featured speaker for that conference and the
conference name

--------------------------
SESSION APIs -- PART OF PROJECT REQUIREMENTS
--------------------------
createSession (PROJECT TASK 3 PART 4):
requires conference Key, allows conference creator to create a session with:
name (required), highlights, speaker, duration (entered in minutes not hours),
typeOfSession (lecture, workshop, lunch, etc), sessDate format (yyyy-mm-dd), and startTime (24 hour clock no seconds)
for example 07:00 is 7am and 19:00 is 7pm.
saves session to Google Datastore.

getConferenceSessions (PROJECT TASK 3 PART 2):
requires conference Key, returns all sessions (all fields) that have been created
for that conference from google Datastore.

getConferenceSessionsByType: (PROJECT TASK 3 PART 2)
requires a conference Key and a typeOfSession (lecture, workshop, etc) returns all sessions
that match that typeOfSession for the given conference.

getConferenceSessionsBySpeaker: (PROJECT TASK 3 PART 3)
requires a speaker's name. returns all sessions for ALL conferences where the provided speaker is the speaker.

getConferenceSessionsByDate: (PROJECT TASK 5 PART 2 - COME UP WITH 2 ADDITIONAL QUERIES)
	REASONING: you have registered for a conference that spans multiple days but due to prior commitments have to miss some days. this endpoint will allow you to see what sessions you will
	be missing and see what sessions you can attend by entering the respective dates.

requires a Conference Key and a date in the format (yyyy-mm-dd) returns all sessions for
provided conference on provided date.

getSessionsByName: (PROJECT TASK 5 PART 2 - COME UP WITH 2 ADDITIONAL QUERIES)
	REASONING: you missed a lecture at a conference and heard rave reviews. This will
	allow you to query all Conferences to see if that lecture will be repeated at
	any other conferences.

requires a session name, returns any sessions from any conference that share that name.

getSessionsBeforeSevenNonWorkshop (PROJECT TASK 5 PART 3 -- SOLVE QUERY PROBLEM)
	PROBLEM: This task poses a problem of quering in a way that Google Datastore does not allow.
	per Google documentation if a != is used to query, no other innequality filters can be used.
	SOLUTION: My solution is to query for all sessions that are not 'workshops', create an empty list
	loop through the returned query object and append all sessions that start before 7pm(19:00) to
	the list. then return that list.

requires nothing, type of Session and startTime are hard coded in python to demonstrate solution.

--------------------------
REGISTRATION
--------------------------
registerForConference:
allows user to register for a conference.

unregisterForConference:
allows user to unregister for a conference

--------------------------
SESSION WISHLIST (PROJECT TASK 4)
--------------------------
addSessionToWishlist: (TASK 4 PART 1)
required session Key adds session to users profile

deleteSessionInWishlist: (TASK 4 PART 3)
reqires session Key. removes session from users profile

getSessionsInWishlist: (TASK 4 PART 2)
returns all sessions in user's profile

--------------------------
TASK QUEUE (PROJECT TASK 6)
	REQUIREMENT: When adding a new session to a conference, determine whether or not the session's speaker should be the new featured speaker. This should be handled using App Engine's Task Queue.

	IMPLEMENTATION: Taskque called when a session is created in _createSessionObject helper method.
	taskque takes 'speaker' and 'websafeConferenceKey' and passes to handler in main.py.
	handler passes speaker and wsck to static method _setFeaturedSpeaker which takes a speaker
	and a websafeKey as arguments, determines if the provided speaker should be the conferences
	featuredSpeaker and if so saves the speaker as featuredSpeaker in the Conference in the datastore.

	getFeaturedSpeaker API is part 2 of this task. implementation is outlined above in
	CONFERENCE APIs section.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

