# What happens when you type https://www.google.com and press Enter?

When you enter `https://www.google.com` in a browser, a full chain of network and server operations starts.

## 1) DNS request
Your browser needs an IP address for `www.google.com`.
- It first checks browser cache and OS DNS cache.
- If not found, it asks a DNS resolver.
- The resolver queries root DNS, `.com` TLD DNS, then Google authoritative DNS.
- The final answer is one or more IP addresses.

## 2) TCP/IP connection
With the IP address known, your browser opens a TCP connection to port `443` (HTTPS).
- TCP 3-way handshake: `SYN` → `SYN-ACK` → `ACK`.
- IP handles routing packets from your machine to Google’s edge servers.

## 3) Firewall checks
Traffic passes through firewalls and security filters:
- Local firewall (your machine/router)
- ISP/network filtering
- Google edge firewalls
Only allowed traffic to HTTPS services continues.

## 4) HTTPS/SSL (TLS handshake)
Before HTTP data is exchanged, TLS handshake happens:
- Server sends certificate.
- Browser validates CA signature, domain name, expiry, and trust chain.
- Client and server negotiate encryption keys.
After this, HTTP traffic is encrypted.

## 5) Load balancer
Your request reaches a load balancer.
- It distributes incoming requests across many backend servers.
- It improves availability and performance.
- It can also route by geo/health/policy.

## 6) Web server
A web server receives the HTTPS request.
- Terminates TLS (or forwards internally).
- Parses HTTP request headers/cookies.
- Serves static assets directly when possible.
- For dynamic pages, forwards to application logic.

## 7) Application server
Application server handles business logic:
- Auth/session checks
- Request processing
- Building response payload (HTML/JSON)
It may call internal services and databases.

## 8) Database
If required, the app queries databases or caches:
- Reads user/session/content data
- Executes indexed queries
- Returns results to app server

## 9) Response back to browser
Server returns HTTP response over encrypted TLS connection.
Browser then:
- Validates response
- Parses HTML
- Requests CSS/JS/images
- Builds DOM/CSSOM
- Executes JS
- Renders final page

In short: DNS resolves the domain, TCP/TLS secures and transports data, firewalls and load balancers protect and distribute traffic, then web/app/database layers build and return the page.
