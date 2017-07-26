# [CarbonDate](http://carbondate.cs.odu.edu)

[![Build Status](https://travis-ci.org/grantat/CarbonDate.svg?branch=master)](https://travis-ci.org/grantat/CarbonDate)
[![codecov](https://codecov.io/gh/grantat/CarbonDate/branch/master/graph/badge.svg)](https://codecov.io/gh/grantat/CarbonDate)

## Prerequisites
* Python 3 only.
* Running in docker container is strongly recommended.
* Install tornado server (to run server).
* Insert your Bitly OAuth access token in config file. Visit https://bitly.com/a/oauth_apps to get your access token.
* Insert your Bing search api key in config file. Visit https://www.microsoft.com/cognitive-services/en-us/bing-web-search-api to get your api key.
* (optional) Change server ip/port number in config.
* All other packages that generate error "No module named" does exist, must be installed.

### Running as a Docker Container

It is recommended to use [Docker](https://www.docker.com/) to install and run this application.

To download the container with docker use:
```
$ docker pull oduwsdl/carbondate
```

Once you have downloaded the container with docker, you can run it as a server or a local command line program.

To run as a server use:
```
$ docker run --rm -it -p 8888:8888 oduwsdl/carbondate ./main.py -s
```
Then you may open your browser to `http://localhost:8888/`.

To run locally use:
```
$ docker run --rm -it -p 8888:8888 oduwsdl/carbondate ./main.py -l search {URI-R}
```

### Running without Docker:

To run it as a server:

```
$ ./main.py -s
```
To CarbonDate `http://example.com`:

Open in a Web browser: `http://localhost:8888/`

To run it as a local script:

```
$ ./main.py -l search URL
```

The backlinks calculation is costly to your computers, so it is recommended to turn it off:

```
$ ./main.py -l search {URI-R} -e cdGetBacklinks
```

## How to add your module:

Name your module main script as cdGet\<Module name\>.py

And ensure the entry function is named  
```
get<Module name>(url,outputArray, indexOfOutputArray,verbose=False,**kwargs)  
```
or customize your own entry function name by assign string value to 'entry' variable in the beginning of your script  
for example your module name is Service,

then the script should be named cdGetService, and interface function should be named  
```
getService (url,outputArray, indexOfOutputArray,verbose=False,**kwargs)  
```

Copy your scripts and to folder ./modules, then the system will automatically detects and loads it.  

### Data returned from your module:

The data returned from your module should be a string of date, in the format like '1995-01-01T12:00:00'  
Put your result date in to outputArray\[indexOfOutputArray\] for result comparasion,  

```
outputArray[outputArrayIndex] = time
```

and put the result and other data you want to show in the "displayArray" like:  
```
kwargs['displayArray'][outputArrayIndex] = time_and_other_data_in_array_of_tuples
```

Where the variable outputArray, indexOfOutputArray and displayArray are past in by the system.  

### If your module has a sub-module:

* If the sub-script is in a subfolder, bring folder with your script, carbon tool will ignore subfolders while loading
* If the sub-script is not in a subfolder, after copying it to ./modules folder, add them into config file, under 'SystemUtility' field

## For more help please visit the [wiki page](https://github.com/DarkAngelZT/CarbonDate/wiki)
