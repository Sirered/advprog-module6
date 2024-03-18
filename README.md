# Module 6

## handle_connection reflection

First, it wraps the stream with a BufReader that can read the contents of the mutable stream inputted into the function. With this buf_reader we can read each line that we got from the stream using a line iterator, mapped. Then we convert the iterator of lines to a String iterator using the map function to unwrap each line in the iterator. Then we take each line from the String iterator until we encounter an empty line. Lastly, we collect the lines that we have taken into the http_request vector. Since the contents of the stream would be the HTTP Request, the created vector would have the information of the HTTP request, line by line, which is then printed to the terminal

## returning_html reflection

First, it uses the same method as before to read the request. Then after it gets and reads the request, the program creates an HTTP Response with the following features:

* A status line that contains the HTTP version, status code and status message

* The Content-length header which describes the length of the content

* Lastly, is the content, which in this case is the html to be served

It creates this response by first storing each of these features separately into different string variables. Afterwards, using string formatting, the program combines all of these features together into one string in the same order as how I listed the features above. The status line and content-length header is separated by one \r\n, while the header section and the content section is separated by 2 \r\ns. Lastly, the program takes this string, and writes this back into the stream, in the form of bytes, so the client is able to get a response with the requested html.
