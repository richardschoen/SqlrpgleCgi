# A sample IBM i SQLRPGLE CGI Program template that uses just built in DB2 SQL and JSON functionality
I haven't done any RPG CGI programming from scratch recently so I wanted to see if I could create a standalone SQLRPGLE CGI JSON data service program that didn't require the use of IWS, YAJL, HTTPAPI, NOXDB or any other RPG frameworks. 

## Setting up for use
- Create your own Apache HTTP server instance. Mine was named: ```WEB3003```.
- View the sample ```httpd.config``` file in this repo for configuration inspiration.
- Compile the ```SQLCGI01``` SQLRPGLE sample CGI program.
- Install postman or your favorite web API testing tool and give it a try.
  

