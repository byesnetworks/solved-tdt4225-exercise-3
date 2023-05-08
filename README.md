Download Link: https://assignmentchef.com/product/solved-tdt4225-exercise-3
<br>
This assignment will look at an open dataset of trajectories, and your task is to create  collections, clean and insert data, and fetch the data to answer some questions. Your  Python program will handle this functionality. The program is inspired by the social  media workout application <a href="https://www.strava.com/features"> </a><a href="https://www.strava.com/features">Strava</a> , where users can track activities like running,  walking, biking etc and post them online with stats about their workout.

Along with this assignment sheet, you have been given several files:

<ul>

 <li>Dataset – Modified dataset based on Geolife GPS Trajectory dataset (please use this dataset, instead of the one from the website. The dataset from the website  contains some files that may give you an error).</li>

 <li>py – a Python class that connects to MySQL on the virtual  machine.</li>

 <li>py – a Python class with examples on how to create tables, insert,  fetch and delete data in MySQL.</li>

 <li>txt – a file containing some pip packages that should be used  in this assignment.</li>

 <li>txt – a file containing the ID of all users who have labeled their  data. This is found in the  dataset.zip  file.</li>

 <li>User-Guide-1.3.pdf –  an official user guide to the Geolife dataset. This is  found in the  zip  file.</li>

</ul>

This assignment is very similar to assignment 2 where you used MySQL. The dataset is  the same, and the tasks are the same. The switch from an SQL-database to a  NoSQL-database is the real challenge here.

<strong> It is <u> strongly</u>  recommended that you read through and understand the whole  assignment sheet before you start solving the tasks. There are also some tips at the  bottom of this assignment, which could be very handy! </strong>

<h1> Dataset – Geolife GPS Trajectory dataset</h1>

<a href="https://www.microsoft.com/en-us/research/publication/geolife-gps-trajectory-dataset-user-guide/"> </a><a href="https://www.microsoft.com/en-us/research/publication/geolife-gps-trajectory-dataset-user-guide/">Geolife GPS Trajectory dataset</a>  is an open source dataset collected by Microsoft from 2007-2011          . This dataset recorded a broad range of users’ outdoor movements,  including not only life routines like going home and going to work but also some  entertainments and sports activities, such as shopping, sightseeing, dining, hiking, and  cycling. The user data is mainly from Beijing, China, but also from the US and Europe.

The dataset is provided in the  dataset.zip  and has some differences from the one  online, for the purpose of this assignment. It contains 182 users that have tracked 18 669             activities in total. Each activity contains a number of GPS-points, which we call  TrackPoints. In total there are over 24 million trackpoints in this dataset.

In the  dataset.zip  you will find the official user guide for the dataset. Be sure to  read through this before you start the task. Here is also a short summary of the  dataset, <u> understanding this is crucial</u>  for completing the assignment:

The folder named Data contains all the 182 users, labeled from “000” to “181”. Each  user has a Trajectory-folder where each activity is stored as a .plt file. Each .plt file  contains several trackpoints.

Line 1…6 in the .plt files are useless in this dataset, and can be ignored. Trackpoints are  described in following lines, one for each line:

Field 1: Latitude in decimal degrees.

Field 2: Longitude in decimal degrees.

Field 3: All set to 0 for this dataset, i.e. you don’t need this field.

Field 4: Altitude in feet (-777 if not valid).

Field 5: Date – number of days (with fractional part) that have passed since  12/30/1899.

Field 6: Date as a string.

Field 7: Time as a string.

Note that field 5 and field 6&amp;7 represent the same date/time in this dataset. You may  use either of them.

Example:

39.906631, 116.385564, 0, 492, 40097.5864583333, 2009-10-11, 14:04:30

39.906554, 116.385625, 0, 492, 40097.5865162037, 2009-10-11, 14:04:35

Some users have also labeled their data with transportation modes. Possible  transportation modes are: <em> walk, bike, bus, taxi, car, subway, train, airplane, boat, run and  motorcycle</em> . We have provided you with the ids of the users that have labeled their data  in  labeled_ids.txt , which will be used for the tasks. The labels contain start time      and end time (both date and time) along with the transportation mode for each activity.

Example:

<strong> Start Time                               End Time                                 Transportation Mode </strong>

2008/04/02 11:24:21               2008/04/02 11:50:45            bus

2008/04/03 01:07:03               2008/04/03 11:31:55            train

<h1> MongoDB – NoSQL</h1>

A quick note on MongoDB and NoSQL. There is some terminology that is different  from the regular relational-database. MongoDB stores data in documents. Documents  are JSON documents based on the JSON specification.  An example of a JSON document would be as follows:

Notice that documents are not just key-value pairs but can include arrays and  subdocuments. The data itself can be different data types like geospatial, decimal,  string etc. This does not have to be pre-defined, neither does two documents in the  same collection have to include the same fields.

A <strong> database </strong> in MongoDB is the container for <strong> collections</strong> . A <strong> collection </strong> is a container for <strong> documents</strong> . This grouping is similar to relational databases and is pictured below:

Source: Robert Walters<em> , ‘Getting Started with Python and MongoDB’, </em> 2017.

Url: <a href="https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb"> </a><a href="https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb">https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb</a>

<h1> Collections</h1>

As mentioned earlier, collections in MongoDB are not as strict as in relational  databases. How you decide to organize your collections and documents is up to you.  The data we are interested in is the same as from Assignment 2 and is displayed in the  figure below. Notice that foreign keys are not really a thing in MongoDB, but it is  optional how you want to reference things in each document.

Because MongoDB offers a lot of ways to handle this, we encourage you to investigate  what solution that might suit the purpose of this assignment best.

Here’s three great articles that we recommend reading before making a decision:

<a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-1"> </a><a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-1">MongoDB Schema Design – Part 1</a> (5      min reading time)

<a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-2"> </a><a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-2">MongoDB Schema Design – Part 2</a> (5      min reading time)

<a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-3"> </a><a href="https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-3">MongoDB Schema Design – Part 3</a> (5      min reading time)

Remember what you did in Assignment 2 and what approach that would fit the tasks.

<table width="600">

 <tbody>

  <tr>

   <td width="159"><strong> User </strong>_id – string  has_labels – boolean</td>

   <td width="224"><strong> Activity </strong>_id – inttransportation_mode – string  start_date_time – datetime  end_date_time – datetime</td>

   <td width="218"><strong> TrackPoint </strong>_id  – int  lat – double  lon – double  altitude – int  date_days – double  date_time – datetime</td>

  </tr>

  <tr>

   <td width="159"> Optional reference  to Activity</td>

   <td width="224"> Optional reference to User  and/or TrackPoint</td>

   <td width="218"> Optional reference toActivity</td>

  </tr>

 </tbody>

</table>

Notice how the id is written as “_id”. In MongoDB, there will always be a “_id” as an  ObjectID if the field is not specified (read more <a href="https://docs.mongodb.com/manual/reference/method/ObjectId/"> </a><a href="https://docs.mongodb.com/manual/reference/method/ObjectId/">here</a>) . E.g., creating a document like  this:

Person = {

id: 1,

name: ‘Name Namesen’

}

would result in a Person-document like this when inserted to the database:

Person = {

_id: ObjectID(‘Some12byteNumber’)  id: 1,

name: ‘Name Namesen’

}

You have to manually override the “_id”-field if you want to set a defined ID (e.g. ‘014’  for Users).

Datetime should be consistent throughout your collections, e.g. in the format  YYYY-MM-DD HH:MM:SS.

<h1> Setup database</h1>

These steps will guide you through how to connect to the virtual machine from your  computer and create a MongoDB-database user with privileges.

<ol>

 <li>First, you need to use NTNU’s VPN to access the virtual machines. Log onto NTNU-VPN with your Feide user (check out <a href="https://innsida.ntnu.no/wiki/-/wiki/English/Install+vpn"> </a><a href="https://innsida.ntnu.no/wiki/-/wiki/English/Install+vpn">this link</a>  if you have not done this  before).</li>

 <li>Open your terminal and enter the following command:</li>

</ol>

ssh <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3841574d4a674d4b5d4a5659555d784c5c4c0c0a0a0d15404016515c5116564c564d165657">[email protected]</a>  where

<strong> “your_username” </strong> is the Feide-username and <strong> “xx” </strong> is your group number for this  project (01, 02, 03… etc).

( If this message pops up, enter <strong> yes</strong> :

The authenticity of host ‘tdt4225-xx.idi.ntnu.no ( xxx.xxx.xxx.xxx)’ can’t be established.

ECDSA key fingerprint is …

Are you sure you want to continue connecting (yes/no)?  yes )

You will then be asked to enter your password, use the Feide-password here.

If the password is correct, you have now successfully logged in!

<ol start="3">

 <li>When using MongoDB, we have to have a server running in one terminal First, type  sudo mkdir -p /data/db , then type       sudo mongod — repair ( both only have to be done the first time you start your server). If  prompted to provide a password, type in your Feide password. Once that is  completed type  sudo mongod –bind_ip_all . If successful, you have now     a running MongoDB-server (the bind_ip_all flag opens for connections from any  IP-address, but don’t worry, we’ll use authentication). This server must be  running whenever you are working with the task. Only one of the group  members has to run the server at a time.</li>

</ol>

<strong> N.B. </strong> if you get error messages running  sudo mongod –repair  or  sudo  mongod –bind_ip_all  it is likely that an instance of mongod is already  running and that you get a problem with unavailable port(s). In this case, try  the following chain of commands:

sudo service mongod restart  sudo systemctl stop mongod  sudo mongod –repair  sudo mongod –bind_ip_all

Continue to step 4

<ol start="4">

 <li>Open a new terminal window and ssh into the virtual machine. Do not close the server-window you have running. To open a client-window for MongoDB type  sudo mongo . Now, you have your MongoDB-server running in one terminal   window, and a MongoDB-client running in the other. If you check your server,  the client-login should’ve been logged there.</li>

 <li>Now we want to create an admin MongoDB-user. The MongoDB-client accepts shell commands written in JavaScript.</li>

</ol>

Start by creating an admin-user by typing the following commands:

&gt;  use admin , this chooses the admin database

&gt;  db.createUser({  user: ‘your_username’,  pwd: ‘your_password’,

roles: [‘root’]

}) , this creates a user with the root-role. Change your_username and  your_password with desired names. The command can be written in one line, it               is spread across several lines here for readability. Here is an example where  your_username=adminuser and pwd=admin123:

&gt;  db.createUser({  user: ‘adminuser’,

pwd: ‘admin123’,  roles: [‘root’]

})

Now type &gt;  show users;  and find your newly created admin user.

<ol start="6">

 <li>Now let’s create the user and the database that the group will use during this To create a database you simply type &gt;  use my_db;  where  my_db is your chosen name. If the database does not exist, it will create it for you. Now do the same command as in Step 5, but with a read/write access-role:</li>

</ol>

&gt;  db.createUser({  user: ‘your_username’,  pwd: ‘your_password’,  roles: [‘readWrite’]

})

Now, your user will have read and write access to the my_db database that you  created. Type &gt;  show users;  and find your newly created user, and check  that the role is correct and attached to the correct database (my_db not admin).  You can also type , but the database will not show until you have created  collections and inserted data into it. Remember to run “use my_db” before  creating the user, so that the user gets access to the correct database.

<ol start="7">

 <li>You can use this client window to create collections etc with the shell   commands, but from now on the Python program will be our MongoDB-client.  Remember to keep the MongoDB-server running.</li>

</ol>

<h1> Setup Python</h1>

We will be using a       <a href="https://api.mongodb.com/python/current/tutorial.html"> </a><a href="https://api.mongodb.com/python/current/tutorial.html"> </a><a href="https://api.mongodb.com/python/current/tutorial.html">MongoDB connector to Python (PyMongo)</a>  in this assignment. If you for some reason would like to complete the assignment in another language, you are            allowed to do so. <strong><em>( NB! We will <u> not</u>  provide support or documentation for other languages,  so we strongly encourage you to use Python.) </em></strong>

With the files provided in this assignment, you will find a requirements.txt,     DbConnector.py   and  example.py , among others.

<ol>

 <li>To set up the required pip-packages for this assignment, simply run   pip install -r requirements.txt  while you are in the directory with  the requirements-file. This will install the connector, along with <a href="https://pypi.org/project/tabulate/"> </a><a href="https://pypi.org/project/tabulate/">tabulate</a> ( used  to print pretty tables in python) and <a href="https://pypi.org/project/haversine/"> </a><a href="https://pypi.org/project/haversine/">haversine</a> ( used to calculate distance  between two coordinates).</li>

 <li>Now, open py  and look at the code. There will be a TODO there  to set up the database correctly with the settings from the database setup.</li>

</ol>

Update the values accordingly:

<strong> Host </strong>=  tdt4225-xx.idi.ntnu.no, where xx is your group number

<strong> Database </strong>=  the name you provided for your database in step 6 of the database  setup (my_db from the example)

<strong> User </strong>=  the username provided in step 6, (not the admin user)

<strong> Password </strong>=  the password provided in step 6

<ol start="3">

 <li>Open py , the file has a main method that creates a connection to the      database from DbConnector, creates a table named “Person”, inserts some  names in the database, displays the data, and then drops the table.  Try to run the code. If everything is set up correctly, you will establish a  connection to the database-server and insert/delete data. You can use this file  for inspiration when solving the tasks in this assignment.</li>

</ol>

<h1> Tasks</h1>

The tasks are divided into three parts: Part 1 will focus on cleaning and inserting the  data into defined tables. Part 2 will focus on writing queries to the database to gain  knowledge of the dataset. Part 3 will focus on writing a report where you discuss your  answers.

We recommend looking at the <a href="https://pymongo.readthedocs.io/en/stable/tutorial.html"> </a><a href="https://pymongo.readthedocs.io/en/stable/tutorial.html">documentation</a> <a href="https://pymongo.readthedocs.io/en/stable/tutorial.html"> </a><a href="https://pymongo.readthedocs.io/en/stable/tutorial.html">f</a>or the MongoDB-Python connector  before you start coding.

<h2> Part 1</h2>

In this task you’ll clean and insert the Geolife dataset into your own MongoDB  database, to  be able to solve the questions in Part 2. In the section “Geolife GPS  Trajectory dataset“ above, you’ll find all the information you need about the dataset  you are handed, and in the section “Collection” you’ll find some nice articles for how to  structure the dataset in your MongoDB database.  Please <u> discuss in your report</u>  how  you structure your collections and documents.

Write a Python program that does the following:

<ol>

 <li>Connects to the MongoDB server on your Ubuntu virtual machine.</li>

 <li>Creates and defines the collections User, Activity and TrackPoint</li>

 <li>Inserts the data from the Geolife dataset into your MongoDB database</li>

</ol>

○  Here, we require a bit of data cleaning and integration. Study the dataset <u> closely</u>  to understand which data goes where.

○  Iterating through the dataset in the directories can be done using <a href="https://www.geeksforgeeks.org/os-walk-python/"> </a><a href="https://www.geeksforgeeks.org/os-walk-python/">os.walk</a>  method, but you are free to use other methods if you find them better for  your solution.

○  When matching transportation_mode from the  labels.txt  files to the  activities, we only consider exact matches on starttime  and end time, i.e.  if you find a match in start time, but not in end time, or vice versa, it  should not be included. Additionally, there are some labeled activities in  labels.txt  that will not have a match amongst the activities.

<strong> ○  Important! </strong> Sometimes it is wise to limit the dataset we’re working with. 24           million TrackPoints is a lot. Therefore we only want you to insert activities that have         <strong> fewer than or exactly 2500 trackpoints </strong> in them, i.e.  when inserting activities into the database, check that the size of the  .plt-files do not exceed 2500 lines (excluding the headers, of course).

When you insert TrackPoints, the same rule applies.

○  Inserting the trackpoints may take a while! Instead of inserting one document of trackpoints at a time, find out if there is a way to insert   bulks of data instead.

<h2> Part 2</h2>

<u> Some of the tasks can be answered using MongoDB-queries only, while some might</u> <u> require both queries and Python code to manipulate the data correctly. </u> Use <a href="https://docs.python.org/3/library/pprint.html"> </a><a href="https://docs.python.org/3/library/pprint.html">pprint</a>  to  pretty-print the data output from MongoDB.

Answer the following questions by writing a Python program using MongoDB-queries

( like in  example.py ):

<ol>

 <li>How many users, activities and trackpoints are there in the dataset (after it is inserted into the database).</li>

 <li>Find the average, minimum and maximum number of activities per user.</li>

 <li>Find the top 10 users with the highest number of activities.</li>

 <li>Find the number of users that have started the activity in one day and ended the activity the next day.</li>

 <li>Find activities that are registered multiple times. You should find the query even if you get zero results.</li>

 <li>An infected person has been at position (lat, lon) (39.97548, 116.33031) at time ‘2008-08-24 15:38:00’.  Find the user_id(s) which have been close to this  person in time and space (pandemic  tracking). Close is defined as the same  minute (60 seconds) and space (100 meters). (This is a simplification of the</li>

</ol>

“unsolvable” problem given i exercise 2).

<ol start="7">

 <li>Find all users that have never taken a taxi.</li>

 <li>Find all types of transportation modes and count how many distinct users that have used the different transportation modes. Do not count the rows where the  transportation mode is null .</li>

 <li>a) Find the year and month with the most activities.</li>

 <li>b) Which user had the most activities this year and month, and how many  recorded hours do they have? Do they have more hours recorded than the user  with the second most activities?</li>

 <li>Find the total distance (in km) <u>walked</u>  in 2008, by user with id=112.</li>

 <li>Find the top 20 users who have gained the most altitude <u>meters</u> .

  <ol>

   <li>Output should be a table with (id, total meters gained per user).</li>

   <li>Remember that some altitude-values are invalid</li>

   <li>Tip: (tpn.altitude-tpn-1.altitude),  altitude &gt;tpn-1.altitude</li>

  </ol></li>

 <li>Find all users who have invalid activities, and the number of invalid activities per user</li>

 <li>An invalid activity is defined as an activity with consecutive trackpoints  where the timestamps deviate with at least 5 minutes.</li>

</ol>

<h2> Part 3</h2>

Write a short report (see  report-template.docx  in the

tdt4225-assignment2.zip)   where you will display and discuss your results from  the tasks. Include screenshots from both part 1 (showing top 10 rows from all of your  tables is sufficient) and part 2 (all the results to each task).

Hand in both the report (as PDF) and your code to BlackBoard within <u> Oct 22, at 16:00<em> .</em></u>

<h1> Tips</h1>

<ul>

 <li>Using the MongoDB terminal on your Ubuntu machine could be useful for checking simple queries without having to use Python and the connector.

  <ul>

   <li>Be sure to have a server running, sudo mongod –bind_ip_all</li>

  </ul></li>

</ul>

○  Open the MongoDB client terminal by typing  sudo mongo , log in with       Feide-password and type use name_of_db     to do this.

<ul>

 <li>Using dictionaries/hashmaps are faster for lookups than lists/arrays in your Python code</li>

 <li>When extracting transportation_mode from the txt  files, remember that you only have to consider the user-ids found in the     labeled_ids.txt     , as    they are the only users where transportation_mode may <u>not </u>  be null.</li>

 <li>Start_time and end_time for activities can be found by looking at the date and time for the first and last trackpoint in each .plt-file</li>

 <li>Use some time to consider the different choices for how to store your data.

  <ul>

   <li>Embedded documents, one-way referencing or  to -way referencing.</li>

  </ul></li>

 <li>Remember to insert data with  the right  Insert integer as int,  date as           some dateformat, etc..

  <ul>

   <li>MongoDB support e.g ISODate</li>

  </ul></li>

 <li>As stated, using <a href="https://pypi.org/project/haversine/">Haversine</a>  for calculating distance is recommended   <a href="https://docs.mongodb.com/manual/reference/sql-comparison/"> </a><a href="https://docs.mongodb.com/manual/reference/sql-comparison/">Comparison</a>  between SQL and  MongoDB.</li>

 <li><a href="https://docs.mongodb.com/manual/reference/sql-aggregation-comparison/">Comparison</a> between SQL-functions and MongoBD-functions.</li>

 <li><a href="https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/">Aggregation</a> and the <a href="https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/"> </a><a href="https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/">pipeline stages for this</a>  are worth checking out.</li>

</ul>

Optional – if you want to visualize the data in the dataset, you