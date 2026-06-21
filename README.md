# Sample SQLRPGLE Web API CGI Program Template
I haven't done any RPG CGI programming from scratch recently so I wanted to see if I could create a standalone SQLRPGLE CGI JSON data service program that didn't require the use of IWS, YAJL, HTTPAPI, NOXDB or any other RPG frameworks.   

This repo contains a functional sample SQLRPGLE CGI program and starter Apache HTTP confguration. The sample IBM i SQLRPGLE CGI Program template just uses the built in DB2 SQL and JSON functionality. 

This type of app data service concept could be used to provide an entirely RPG based back-end data service for other multiplatform web app servers, web applications or mobile apps without needing to expose additional SQL data services such as ODBC, JDBC or tools like Mapepire which all allow SQL to be directly executed.  

While it needs some work this is a good starting point for an RPG CGI Web Service API.   

## Benefits of a standalone CGI program
- No outside libraries or frameworks required.
- No deployment other than compile and go.
- No IWS server needed for deployment.
- Uses standard Apache web server configuration.
- Direct RPG calls are super-fast.
- Re-use any existing RPG, CL or other callable OPM or ILE programs.

## Features of the program
- Uses DB2 for all SQL data queries.
- Uses SQL and JSON_TABLE to parse the posted JSON parameter data for use.
- Allows running of CL commands if the appropriate setting is enabled.

## Setting up for use
- Create your own Apache HTTP server instance. Mine was named: ```WEB3003```.
- View the sample ```httpd.config``` file in this repo for configuration inspiration.
- Compile the ```SQLCGI01``` SQLRPGLE sample CGI program.
- Install postman or your favorite web API testing tool and give it a try.
  
## Techical things I learned
- I set up the program to always use a *NEW activation group to get a unique program instance. I was getting data left over in the request buffers. Where I saw it was when I tried running a CL command. If I didn't clear the buffer before the command call and the next command was shorter than the previous it would sometimes show as null until I fixed it by clearing the incoming buffers or uses activation group *NEW to force a new program instance to run.
- If I didn't do the above I needed to manually clear the data buffers for incoming requests, even when I set the *LR indicator on before exiting. It would appear even with *LR on and the the program running in the same activation group that the program never really unloaded. (at least the incoming memory buffers. Perhaps those are tied to the actual CGI job). Perhaps bigger minds than mine can analyze this better, but using activation group *NEW or clearing incoming stdin buffers manually before use seems to have resolved the issue for now.
- The Apache server requires special rewrite settings in order to pass the Authorization header. It also passes the actual header value as ```HTTP_AUTHORIZATION``` and not ```Authorization``` to the CGI program.

## Try it and contribute back your examples
If you use or adapt this program please contribute back so others can learn and benefit from using SQLRPGLE programs as CGI apps to provide super fast HTTP based RESTful/RESTlike Web APIs and database services using your existing RPG and CL programs. 
