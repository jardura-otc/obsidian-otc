[Curl docs](https://everything.curl.dev)

```shell
# Get help
curl --help

# GET
curl <url>
curl https://jsonplaceholder.typicode.com/posts/1
# Save into a file
curl -o <path-to-save> <url>
curl -o ./hsploit.html https://hsploit.com
```

>[!tip]
>You can save a file with curl too. Just check the download URL and save it to your computer. 
>

```shell
# Download a file with its original name
curl -O <url>

# Redirect
curl -L <url>

# Query the response from the webserver
curl -I <url>

# TLS handshake
curl -v https://otcengineering.com
```

---
### Rest API
```shell
# GET
curl <url>

# POST - Make sure that the format is acceptable
curl -d <body> -H <Content-Type> .X POST <url>

# PUT
curl -d <body> -H <Content-Type> .X PUT <url>

# DELETE
curl -X DELETE <url>

```