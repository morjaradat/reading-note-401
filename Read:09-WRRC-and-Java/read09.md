# The HTTP Request Lifecycle

## Step 1: Local Processing

- the browser will make Schema for the request and contain protocol,host ,port number, resource path, and query then the browser will resolve an IP address then its ready to send the request

## Step 2: Resolve an IP

- if the cache lookup success the browser fires off DNS request using UDP3,The DNS request have your return IP in its header

- the request will  travel throws many network devices to reach its target DNS server,when its reach the network he will use the  routing table to see which other devices is connected

- when the request arrives to the server ,the server will look to your address associated that have  the requested hostname ,if it find one then it will send response if not the DSN server cannot locate hostname then its pass he request to another DNS until he find one ,if he cannot find one he response with a failure and your browser returns an error.

- if the request was successful then the requesting client  has a target IP it will receive a part of information an tell you the how long will take to response

## Step 3: Establish a TCP Connection

- the browser must open an TCP connection(transport layer protocol).

- One of the differences between TCP and UDP is that TCP ensures delivery and ordered data transmission by using  sequence number for every byte sent,this allow the receiver to re-order the request

- TCP connections are opened using three ways called three-way handshake :

1. The client initiates the active open by sending a SYN7 "control to the server
2. The server responds with a SYN-ACK9 message,
3. the client sends an ACK10 message back to the server with a sequence number equal to x+1 which should mean the data has been delivery.

## Step 4: Send an HTTP Request

- The request is made up of a(request line), request header and a body.
- The request line its line taht indicates the HTTP method.
- The header of the request is made up of pairs in the form name:value CR and LF
- both CR and LF indicate the end of the header section
- Host which contain both domain and port taht the request is sended to .
- common standard HTTP header fields include Origin, Accept, Accept-Encoding.
- the body content of an HTTP request is completely optional but we prefer to send the data in json format.
- when the HTTP request is sent and  in correct way the server will process the request and send back an response .

## Step 5: Tearing Down and Cleaning Up

- when the response success the client will send a FIN packet and the server will response with ACK packet then server will waits for a brief timeout, during which it cannot accept new connections to prevent delayed packets

# Do a Simple HTTP Request in Java

## way of performing HTTP requests in Java by using the built-in Java class HttpUrlConnection.

### HttpUrlConnection

- its class that allows us to perform basic HTTP requests without the use of any external libraries
- The HttpUrlConnection class is used for all types of requests by setting a requests method in the value .

``
URL url = new URL("http://example.com");

HttpURLConnection con = (HttpURLConnection) url.openConnection();

con.setRequestMethod("GET");
``

### Adding Request Parameters

- we can add parameters to a request by setting the doOutput property to true then write the parameters in OutputStream 

```
Map<String, String> parameters = new HashMap<>();
parameters.put("param1", "val");

con.setDoOutput(true);
DataOutputStream out = new DataOutputStream(con.getOutputStream());
out.writeBytes(ParameterStringBuilder.getParamsString(parameters));
out.flush();
out.close()
```

- To facilitate the transformation of the parameter Map, we have written a utility class called ParameterStringBuilder containing a static method, getParamsString(), that transforms a Map into a String of the required format

```
public class ParameterStringBuilder {
    public static String getParamsString(Map<String, String> params) 
      throws UnsupportedEncodingException{
        StringBuilder result = new StringBuilder();

        for (Map.Entry<String, String> entry : params.entrySet()) {
          result.append(URLEncoder.encode(entry.getKey(), "UTF-8"));
          result.append("=");
          result.append(URLEncoder.encode(entry.getValue(), "UTF-8"));
          result.append("&");
        }

        String resultString = result.toString();
        return resultString.length() > 0
          ? resultString.substring(0, resultString.length() - 1)
          : resultString;
    }
}
```

### Setting Request Headers

- by using the setRequestProperty() method
- To read the value of a header from a connection, we use the getHeaderField() method

```
con.setRequestProperty("Content-Type", "application/json");
String contentType = con.getHeaderField("Content-Type");
```

### Configuring Timeouts

- HttpUrlConnection class allows setting the connect and read timeouts its like await ti wait the response from the server .

```
con.setConnectTimeout(5000);
con.setReadTimeout(5000);
```

### Handling Cookies

1. read the cookies from a response

```
String cookiesHeader = con.getHeaderField("Set-Cookie");
List<HttpCookie> cookies = HttpCookie.parse(cookiesHeader);
```

2. add the cookies to the cookie store:

```
cookies.forEach(cookie -> cookieManager.getCookieStore().add(null, cookie));
```

- if a cookie called username is present, and if not, we will add it to the cookie store with a value of “john”:

```
Optional<HttpCookie> usernameCookie = cookies.stream()
  .findAny().filter(cookie -> cookie.getName().equals("username"));
if (usernameCookie == null) {
    cookieManager.getCookieStore().add(null, new HttpCookie("username", "john"));
}
```

3. add the cookies to the request

```
con.disconnect();
con = (HttpURLConnection) url.openConnection();

con.setRequestProperty("Cookie", 
  StringUtils.join(cookieManager.getCookieStore().getCookies(), ";"));
```

### Handling Redirects

- we can handle it by enable or disable automatically following redirects for a specific connection by using the setInstanceFollowRedirects() method.

```
con.setInstanceFollowRedirects(false);
```

- we can enable and disable automatic redirect for all connections (by default its enable)

```
HttpUrlConnection.setFollowRedirects(false);
```

### Reading the Response

- we can read the response by parsing the InputStream of the HttpUrlConnection instance.

- To execute the request, we can use the getResponseCode(), connect(), getInputStream() or getOutputStream() methods:

```
int status = con.getResponseCode();
```

- read the response :

```
BufferedReader in = new BufferedReader(
  new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer content = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    content.append(inputLine);
}
in.close();
```

- To close the connection, we can use the disconnect() method:

```
con.disconnect();
```

### Reading the Response on Failed Requests

- If the request fails the HttpUrlConnection instance won't work then we can use  consume the stream provided by HttpUrlConnection.getErrorStream().
- We can decide which InputStream to use by comparing the HTTP status code:

```
int status = con.getResponseCode();

Reader streamReader = null;

if (status > 299) {
    streamReader = new InputStreamReader(con.getErrorStream());
} else {
    streamReader = new InputStreamReader(con.getInputStream());
}
```

### Building the Full Response

- we can build it using some of the methods that the HttpUrlConnection by:

```
public class FullResponseBuilder {
    public static String getFullResponse(HttpURLConnection con) throws IOException {
        StringBuilder fullResponseBuilder = new StringBuilder();

        // read status and message

        // read headers

        // read response content

        return fullResponseBuilder.toString();
    }
}
```

- adding the response status information :

```
fullResponseBuilder.append(con.getResponseCode())
  .append(" ")
  .append(con.getResponseMessage())
  .append("\n");
```

- then get the header by using getHeaderFields() 

```
con.getHeaderFields().entrySet().stream()
  .filter(entry -> entry.getKey() != null)
  .forEach(entry -> {
      fullResponseBuilder.append(entry.getKey()).append(": ");
      List headerValues = entry.getValue();
      Iterator it = headerValues.iterator();
      if (it.hasNext()) {
          fullResponseBuilder.append(it.next());
          while (it.hasNext()) {
              fullResponseBuilder.append(", ").append(it.next());
          }
      }
      fullResponseBuilder.append("\n");
});
```

- then read the response content as we did previously and append it
