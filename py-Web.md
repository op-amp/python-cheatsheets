# Python Web Scraping


###### _Table of Contents_

- Opening Webpage
- Making Requests
	1. Requests
	2. Responses
	3. Status Codes
- Parsing Web Documents


## Opening Webpage

The **`webbrowser` module** allows displaying web-based documents to users.

`webbrowser.open(url, new=0, autoraise=True)` opens a webpage specified by the _url_ string using the default browser.

- If _new_ is 0, in the same browser window;
- If _new_ is 1, in a new browser window;
- If _new_ is 2, in a new browser tab.


## Making Requests

The **`requests` module** offered by the third-party package [`requests`](https://requests.readthedocs.io/en/latest/api/)
is a Python HTTP library. Install through the terminal by:

```bash
python -m pip install requests
```

### Requests

1. `requests.get(url, params=None)` sends a GET request.
    - _params_ can be a dictionary, list of tuples, or bytes to send in the query string.
2. `requests.head(url)` sends a HEAD request.
3. `requests.post(url, data=None, json=None)` sends a POST request.
    - _data_ can be a dictionary, list of tuples, bytes, or `file` object to send in the request body.
    - _json_ should be a JSON serializable Python object to send in the request body.
4. `requests.put(url, data=None)` sends a PUT request.
5. `requests.delete(url)` sends a DELETE request.
6. `requests.patch(url)` sends a PATCH request.

### Responses

All requests from the `requests` module returns a [`requests.Response`](https://requests.readthedocs.io/en/latest/api/#requests.Response) object.

**Status**

1. `res.url` is the final URL location of response.
2. `res.status_code` is the integer code of responded HTTP status.
3. `res.reason` is the textual reason of responded HTTP status.
4. `res.raise_for_status()` raises `HTTPError`, if one occurred.

**Content Access**

1. `res.encoding` is the encoding to decode with when accessing `text()` property.
2. `res.text` is the content of the response, in text.
3. `res.content` is the content of the response, in bytes.
4. `res.json()` returns the json-encoded content of a response utilizing `json.loads`.

**Content Iteration**

1. `res.iter_content(chunk_size=1)` iterates over the response data, with each time _chunk_size_ bytes read into memory.
2. `res.iter_lines(chunk_size=512, delimiter=None)` iterates over the response data line by line.

### Status Codes

[`requests.codes`](https://requests.readthedocs.io/en/latest/api/#status-code-lookup)
is an object defining a mapping from common names for HTTP statuses to numerical codes.


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
