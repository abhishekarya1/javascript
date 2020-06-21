# JSON
The JSON (JavaScript Object Notation) is a general format to represent values and objects. It is described as in RFC 4627 standard. Initially it was made for JavaScript, but many other languages have libraries to handle it as well. So it's easy to use JSON for data exchange when the client uses JavaScript and the server is written on Ruby/PHP/Java/Whatever.

JavaScript provides methods:
- `JSON.stringify` to convert objects into JSON.
- `JSON.parse` to convert JSON back into an object.

## JSON.stringify
The method JSON.stringify(student) takes the object and converts it into a string.

The resulting json string is called a JSON-encoded or serialized or stringified or marshalled object. We are ready to send it over the wire or put into a plain data store.
