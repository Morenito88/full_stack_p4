Conference Central  Version 1.2  11/19/2015

Requirements
------------
To a full success use of Conference Central you need:

    o App Engine
    o Python 2.7
    o Google Cloud Endpoints

Installation
------------

1. Update the value of  application  in  app.yaml  to the app ID you have registered in the App Engine admin console.

2. Update the values at the top of  settings.py  to reflect the respective client IDs you have registered in the Developer Console.

3. Update the value of CLIENT_ID in  static/js/app.js  to the Web client ID (line 89).

4. Run the app with the Google App Engine Launcher. 

5. Ensure it's running by visiting your local server's address (by default localhost:8080).

6. Deploy your application.

    
Design Choices
------------

Task 1: Add Sessions to a Conference

   * Session is defined as a pure entity with Conference entity as ancestor.
    Sessions can contain multiple Speakers identified by their email. 
    The 'startTime' is a DateTime field and must be addressed in the format HH:MM in 24hr UTC format.
    The 'typeOfSession' is a string field that can contain any kind of text. In the future could be replaced with a ENUM type of field.
    Beside that it also have 'name', 'highlights', 'duration' and 'date'.
   
   * Speaker is defined as a pure entity with 'name', 'email', 'areasOfStudy' and 'webpage' fields.
    I've choosed to use the 'email' as identifier because make it easier to shearch for a specific user, just using is email (easier to remind)


Task 2: Add Sessions to User Wishlist

   * The wishlist stores the key of sessions in the user profile. The user can only add a session to their wishlist if he register in the conference.


Task 3: Work on indexes and queries

   * I've implemented 3 new queries:
    1. getMorningSessions() - returns all the sessions that starts between 8am and 1pm
    2. getShortWorkshopSessions() - return all the sessions of type 'Workshop' where the duration is less than 30 minutes
    3. query problem - Datastore does not permit inequality filters on more than one field., and by default this needs two (typeOfSession and startTime). One possible solution is to break this into two querys: first filtering the session by time and then remove the keys of all with the undesired type, then finally querying and returning the sessions from the remaining keys. This is implemented in filteredSession().


Task 4: Add a Task

   * Featured Speaker - A memcache entry is created when creating a new session and the speaker in question will have two or more sessions.
 

Licensing
---------

Please see the file LICENSE.

Contacts
--------

o If you want to be informed about new code releases, bug fixes,
security fixes, general news and information about the Conference Central project just keep tracking this repository.

o If you want freely available support for this script 
or any kind of help just mail <hugophp@sapo.pt>

