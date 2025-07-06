| Code | Meaning | ELI5 | Pentesting Tip |
|------|---------|------|----------------|
| 100 | Continue | The server is saying: 'Cool, keep going!' | You might see this during long POSTs or chunked uploads. |
| 101 | Switching Protocols | The server is changing the communication protocol as requested. | Used in WebSocket upgrades. |
| 200 | OK | Everything went fine! | Most common success response. |
| 201 | Created | Your request created something new. | Useful in REST APIs for resource creation. |
| 202 | Accepted | The server got it, but it's still working on it. | Check back later – async ops. |
| 204 | No Content | Request succeeded but nothing to show. | After DELETE requests or API pings. |
| 301 | Moved Permanently | The thing you asked for moved forever. | Follow the redirect – good to know for phishing redirection. |
| 302 | Found | It moved temporarily. | Temporarily redirected; sometimes used in login redirection. |
| 304 | Not Modified | Nothing changed since last time. | Browser uses cached copy – useful when testing caching headers. |
| 400 | Bad Request | You messed up the request. | Try malformed input – can sometimes break logic. |
| 401 | Unauthorized | You need to log in. | Bruteforce or auth bypass targets. |
| 403 | Forbidden | You're not allowed. | Good sign there’s something juicy behind it. |
| 404 | Not Found | It doesn’t exist. | Fuzzing target – what pages exist and what don't. |
| 405 | Method Not Allowed | You can't use that method here. | Test other HTTP verbs like PUT/DELETE. |
| 407 | Proxy Authentication Required | Need auth for the proxy. | Rare in public apps, interesting in corp networks. |
| 408 | Request Timeout | You were too slow. | Can be used in slowloris-style DoS attacks. |
| 409 | Conflict | There’s a data conflict. | Occurs in race conditions – check how app handles concurrency. |
| 410 | Gone | It used to be there but now it's gone. | Less common than 404, but means it was removed intentionally. |
| 413 | Payload Too Large | You sent too much data. | Can be useful for buffer overflow/DoS testing. |
| 414 | URI Too Long | Your URL is massive. | Useful when testing for input length handling. |
| 418 | I'm a teapot | It's a joke code from an April Fools’ RFC. | Sometimes left in as easter eggs. |
| 429 | Too Many Requests | You're being rate-limited. | Throttling – time to back off or rotate IPs. |
| 500 | Internal Server Error | The server broke while handling your request. | Great for finding bugs and logic errors. |
| 501 | Not Implemented | Server doesn't know how to do that. | Uncommon – could be an edge case or misconfig. |
| 502 | Bad Gateway | Server got a bad response from upstream. | Can appear during SSRF or upstream testing. |
| 503 | Service Unavailable | Server is overloaded or down for maintenance. | Test during high load or DoS. |
| 504 | Gateway Timeout | Upstream server didn’t reply in time. | Another angle for SSRF or upstream enumeration. |
| 505 | HTTP Version Not Supported | That HTTP version is too old or not allowed. | Interesting for protocol downgrade attacks. |