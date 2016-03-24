# restc-cpp

This is a minimalistic but still functioning and very fast
(at least, that is the intention) HTTP/HTTPS client library in C++.

It depends on C++14 with its standard libraries and boost.
It uses boost::asio for IO.

The library is written by Jarle (jgaa) Aase, an enthusiastic
C++ software developer since 1996. (Before that, I used C).

## Design Goal
The design goal of this project is to make external REST API's
simple to use in C++ projects, but still very fast (which is why
we use C++ in the first place, right?).

Usually I use some version of GPL or LGPL for my projects. This
library however is so tiny and general that I have released it
under the more permissive MIT license.

## Example

The following code is all that is needed to run REST requests asynchronously,
using the co-routine support in boost::asio behind the scenes. (To see how
this works, please see my
[modern async cpp example](https://github.com/jgaa/modern_async_cpp_example)).


```C++
#include <iostream>
#include "restc-cpp/restc-cpp.h"

using namespace std;
using namespace restc_cpp;

void DoSomethingInteresting(Context& ctx) {

    // Asynchronously connect to a server and fetch some data.
    auto reply = ctx.Get("http://jsonplaceholder.typicode.com/posts");

    // Asynchronously fetch the entire data-set and return it as a string.
    auto json = reply->GetBodyAsString();

    // Just dump the data.
    clog << "Received data: " << json << endl;
}

main(int argc, char *argv[]) {
    auto rest_client = RestClient::Create();
    rest_client->Process(DoSomethingInteresting);

    // Hold the main thread...
    cin.get();
}
```


## Current Status
The project is justs starting up.

The code is immature and not properly tested, but capable of executing
simple REST requests.


## Supported development platforms:
- Linux (Debian stable and testing)
- Windows 10 (Latest "community" C++ compiler from Microsoft

## Suggested target platforms:
- Linux
- OS/X
- Android (via NDK)
- Windows Vista and later
- Windows mobile


## Short Term Tasks
- [x] ~~Implement GET, POST, PUT, DELETE~~~
- [x] ~~Implement HTTPS~~
- [ ] Implement connection pool
- [ ] Implement Chunked Reponse handling
- [ ] Implement Chunked Requests
- [ ] Implement simple File Upload (as body)
- [ ] Implement simple File Download (from body)
- [ ] Verify that it compiles with Debian Stable
- [ ] Verify that it compiles with Windows 10 / Visual Studio
- [ ] Verify that it compiles with OS/X
- [ ] Implement Mime multipart Requests
- [ ] Implement Mime multipart Responses
- [ ] Implement Form Data encoding (with File Upload)
- [ ] Implement asynchronous iterators for received data and integrate with json parser.
- [ ] Implement asynchronous iterators for requests data and integrate with json generator.
- [ ] Add options to secure TLS connections (avoid weak encryption and verify server certs).
