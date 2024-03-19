# Module 6

## handle_connection reflection

First, it wraps the stream with a BufReader that can read the contents of the mutable stream inputted into the function. With this buf_reader we can read each line that we got from the stream using a line iterator, mapped. Then we convert the iterator of lines to a String iterator using the map function to unwrap each line in the iterator. Then we take each line from the String iterator until we encounter an empty line. Lastly, we collect the lines that we have taken into the http_request vector. Since the contents of the stream would be the HTTP Request, the created vector would have the information of the HTTP request, line by line, which is then printed to the terminal

## returning_html reflection

![image](https://github.com/Sirered/advprog-module6/assets/126568984/844b85c6-75a7-492c-a440-7240a142c2b0)

First, it uses the same method as before to read the request. Then after it gets and reads the request, the program creates an HTTP Response with the following features:

* A status line that contains the HTTP version, status code and status message

* The Content-length header which describes the length of the content

* Lastly, is the content, which in this case is the html to be served

It creates this response by first storing each of these features separately into different string variables. Afterwards, using string formatting, the program combines all of these features together into one string in the same order as how I listed the features above. The status line and content-length header is separated by one \r\n, while the header section and the content section is separated by 2 \r\ns. Lastly, the program takes this string, and writes this back into the stream, in the form of bytes, so the client is able to get a response with the requested html.


## Validating request and selectively responding reflection

![image](https://github.com/Sirered/advprog-module6/assets/126568984/15602516-ccf8-4f5b-81c9-41d3d42b43a6)


To split between how to process a request and what response is given for such, we have to check the status line, specifically the URI. The URI is the second parameter of the status line of a request and is the content of the URL after the info regarding the destination of the request (so it's the part of the URL that may differ even if the requests go to the same website). We use this URI to differentiate the types of request that is being asked, thus to differentiate responses we just have to check the URI. In this example we only treat the URI '/' as a valid request, hence if the status line is 'GET / HTTP/1.1' then we give them the normal hello.html, with a success status code. If it is anything else, that means that it is an invalid URI, in which case we return an error not found status code and error page.

The difference between how a valid and invalid error is processed is the filename of the html that will be served and the status code in the status line. Thus instead of having to have the same exact code for each different type of response, except for the inputted fine name and status line, we can just set the filename and status line according to the URI (and since other than those variables, the processing is the same) then process the filename and status line the same. This refactoring cuts down on unnecessary duplicate code. 

## Simulation of slow request reflection

The reason why the response for the URI '/' was delayed was because of the fact that it has to wait for the response for '/sleep' to finish first. The way that the program serves requests is by waiting for an incoming stream, processes it then continues to the next incoming stream (if there are any remaining). This causes delays to other requests that shouldn't take long, because the program has to finish processing (or in the case of the /sleep end point, sleeping) before it can start working on the next request, regardless of how quick the next request should take to process