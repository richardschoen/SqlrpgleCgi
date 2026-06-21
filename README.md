# Sample SQLRPGLE CGI Program Template
I haven't done any RPG CGI programming from scratch recently so I wanted to see if I could create a standalone SQLRPGLE CGI JSON data service program that didn't require the use of IWS, YAJL, HTTPAPI, NOXDB or any other RPG frameworks.   

This repo contains a functional sample SQLRPGLE CGI program and Apache HTTP confguration. The sample IBM i SQLRPGLE CGI Program template just uses the built in DB2 SQL and JSON functionality.  

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
- I set up the program to always use a *NEW activation group to get a unique program instance.
- If I didn't do the above I needed to manually clear the data buffers for incoming requests, even when I set the *LR indicator on before exiting. It would appear even with *LR on and the the program running in the same activation group that the program never really unloaded. (at least the incoming memory buffers. Perhaps those are tied to the actual CGI job). Perhaps bigger minds than mine can analyze this better, but using activation group *NEW or clearing incoming stdin buffers manually before use seems to have resolved the issue for now.
- The Apache server requires special rewrite settings in order to pass the Authorization header. It also passes the actual header value as ```HTTP_AUTHORIZATION``` and not ```Authorization``` to the CGI program.  
