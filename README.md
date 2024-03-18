# Module 6

## handle_connection reflection

First, it wraps the stream with a BufReader that can read the contents of the mutable stream inputted into the function. With this buf_reader we can read each line that we got from the stream using a line iterator, mapped. Then we convert the iterator of lines to a String iterator using the map function to unwrap each line in the iterator. Then we take each line from the String iterator until we encounter an empty line. Lastly, we collect the lines that we have taken into the http_request vector. Since the contents of the stream would be the HTTP Request, the created vector would have the information of the HTTP request, line by line, which is then printed to the terminal
