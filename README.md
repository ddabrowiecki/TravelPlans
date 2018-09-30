# Travel Destinations

A simple app to keep track of destinations I'd like to visit.

#Monthly Report Project#

##Overview##

These files serve as a project for the Full Stack Nanodegree with Udacity.  Given a news database with several tables, I determined most popular articles and authors as well as the days of one month on which more than 1% of pageviews resulted in an error.

##Installation##

This project must be run from a virtual machine.  Visit [this link](https://www.vagrantup.com/) to install Vagrant.

Once you are running the virtual machine, change directory to the directory containing the file and run the program on the command line.

The enclosed .txt file has the results of the queries in an easy to read format.

##Views##

To solve the problem, I created several views using PostgreSQL.  Below, you can access these views with the following code snippets:

Updated Articles Table

`
cursor.execute("create view updated_articles_table as select * from log;")
cursor.execute("update updated_articles_table set path = 'Candidate is jerk, alleges rival' where path like '/article/candidate%';")
cursor.execute("update updated_articles_table set path = 'Bad things gone, say good people' where path like '/article/bad%';")
cursor.execute("update updated_articles_table set path = 'Bears love berries, alleges bear' where path like '/article/bears%';")
cursor.execute("update updated_articles_table set path = 'Goats eat Google''s lawn' where path like '/article/goats%';")
cursor.execute("update updated_articles_table set path = 'Trouble for troubled troublemakers' where path like '/article/trouble%';")
cursor.execute("update updated_articles_table set path = 'There are a lot of bears' where path like '/article/so-many%';")
cursor.execute("update updated_articles_table set path = 'Balloon goons doomed' where path like '/article/balloon%';")
cursor.execute("update updated_articles_table set path = 'Media obsessed with bears' where path like '/article/media%';")
`

Number of Article Views

`
cursor.execute("create view numarticleviews as select count(*), path from log group by path order by count(*) desc;")
`

Errors by Day

`
cursor.execute("create view daily_errors as select date_trunc('day',time) day_of_month,count(status) filter (where status = '404 NOT FOUND') as error,count(status) as total from log group by day_of_month order by day_of_month asc;")
`

Errors Greater Than One Percent

`
cursor.execute("create view errors_greater_than_one as select day_of_month,(error*100.0)/(total*100.0) as percentage_errors from daily_errors group by day_of_month,error,total order by day_of_month asc;")
`


