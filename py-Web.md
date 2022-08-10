# Python Web Scraping


###### _Table of Contents_

- Opening Webpage
- Making Requests
	1. Requests
	2. Responses
	3. Status Codes
- Parsing Web Documents
	1. Initializing HTML
	2. CSS Selectors
	3. Tag Features


## Opening Webpage

The **`webbrowser` module** allows displaying web-based documents to users.

`webbrowser.open(url, new=0, autoraise=True)` opens a webpage specified by the _url_ string using the default browser.

- If _new_ is 0, in the same browser window;
- If _new_ is 1, in a new browser window;
- If _new_ is 2, in a new browser tab.


## Making Requests

The **`requests` module** is offered by the third-party package [`requests`](https://requests.readthedocs.io/en/latest/api/),
which is a Python HTTP library. Install through the terminal by:

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

**Content**

1. `res.encoding` is the encoding to decode with when accessing `text()` property.
2. `res.text` is the content of the response, in text.
3. `res.content` is the content of the response, in bytes.
4. `res.iter_content(chunk_size=1)` iterates over the response data, with each time _chunk_size_ bytes read into memory.
5. `res.json()` returns the json-encoded content of a response utilizing `json.loads`.

### Status Codes

[`requests.codes`](https://requests.readthedocs.io/en/latest/api/#status-code-lookup)
is an object defining a mapping from common names for HTTP statuses to numerical codes.

```python
import requests
res = requests.get(url)
if res.status_code == requests.codes['ok']:
    file = open(path, 'wb')
    for chunk in res.iter_content(1024):
        file.write(chunk)
    file.close()
```


## Parsing Web Documents

[Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) with the **`bs4` module**,
is a library for extracting information from an HTML page. Install by:

```bash
python -m pip install beautifulsoup4
```

### Initializing HTML

```python
import bs4
soup = bs4.BeautifulSoup(document, 'html.parser')
```

`bs4.BeautifulSoup(document, parser)` takes in a string or an open `file` object and returns a `BeautifulSoup` object.

### CSS Selectors

`soup.select(selector)` takes in a string of a CSS selector and returns a list of `Tag` objects.

| Purpose | Syntax |
|---------|--------|
| Type selector      | `tag`
| Class selector     | `.class`
| ID selector        | `#id`
| Attribute selector | `[attr]` `[attr=value]`
| Grouping selectors | `,`
| Descendant combinator | ` `
| Child combinator      | ` > `
| General sibling combinator  | ` ~ `
| Adjacent sibling combinator | ` + `
| Pseudo classes  | `:`
| Pseudo elements | `::`

### Tag Features

**Name**

`tag.name` is the name of the HTML element tag.

**Attributes**

`tag.attrs` is the dictionary containing the attributes with values.

For simplicity, access the attributes of a tag by treating the `Tag` objects like a dictionary.


## *References*
Sweigart, A. (2015). _Automate the Boring Stuff With Python: Practical Programming for Total Beginners_. San Francisco, CA: No Starch Press.
