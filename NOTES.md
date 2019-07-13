# Quick! Spring Boot + Database + Freehosting = great starting point

1. Some random googling took me to this tutorial: https://devcenter.heroku.com/articles/getting-started-with-gradle-on-heroku
2. So I cloned https://github.com/heroku/gradle-getting-started and made a few changes: https://github.com/payne/gradle-getting-started/commits/master
3. Since I already had a no-cost heroku.com account and the heroku cli installed on my WSL in Windows 10 home I was able to run
4. `heroku create`  inside the git repo I forked.
5. `heroku addons:create heroku-postgresql:hobby-dev` to add a free postgresql.org database instance
6. `git push heroku master` to deploy and start up the application.
7. `heroku open` failed to open a web browser (I have my heroku CLI installed in WSL 1 after all), but it did tell me the URL of my app:
8. https://guarded-caverns-67543.herokuapp.com/db 
9. `heroku psql` runs a local postgreSQL prompt connected to the database server on heroku.   So I can have a session like this:
```
mpayne@Payne:/mnt/c/Users/Payne/cs/gradle-getting-started$ heroku psql
--> Connecting to postgresql-silhouetted-15757
psql (10.6 (Ubuntu 10.6-0ubuntu0.18.04.1), server 11.3 (Ubuntu 11.3-1.pgdg16.04+1))
WARNING: psql major version 10, server major version 11.
         Some psql features might not work.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.

guarded-caverns-67543::DATABASE=> select * from ticks;
            tick
----------------------------
 2019-07-13 23:17:03.828392
 2019-07-13 23:17:07.871997
(2 rows)

guarded-caverns-67543::DATABASE=> \q
```
Yes, it's `\q` to quit.


## Local -- h2database.com
1. I added h2 to the build.gradle and created an application-local.properties file so I can run `SPRING_PROFILES_ACTIVE=local gradle bootRun` when I do this, the settings in application-local.properties over ride those in application.properties (which are set first).  So, the application listens on 8080
and is using h2.   Sadly, I don't know why the h2 console bit is not working.  :-(

