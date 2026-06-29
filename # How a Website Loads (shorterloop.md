#   How a Website Loads (shorterloop.com)

## Ever wonder what actually happens when you open a website?
## Typing a URL feels instant but it's not — here's everything that actually happens behind the scenes.

**1. DNS Lookup**
My browser only knows the name, not the IP, so it asks DNS to find the real address. I checked this with `nslookup shorterloop.com` and got `199.36.158.100`.


<img width="200" height="230" alt="Screenshot 2026-06-24 210011" src="https://github.com/user-attachments/assets/7dfafc29-c83b-4f06-866b-3334b75ea92d" />


**2. TCP Handshake**
The browser connects to that IP using TCP — a quick back-and-forth to confirm both sides are ready before sending any real data./>


<img width="200" height="230" alt="Screenshot 2026-06-24 212353" src="https://github.com/user-attachments/assets/2d67979e-c8be-4e7d-aa30-f1a975800f1b" />



**3. TLS Handshake**
Since it's HTTPS, the browser and server also agree on encryption here, so the connection stays secure. That's the lock icon next to the URL.


<img width="200" height="300" alt="Screenshot 2026-06-24 210606" src="https://github.com/user-attachments/assets/41fb595f-dc41-417f-9a01-ca12226f77e9" />



**4. HTTP Request**
The browser sends a GET request asking for the homepage. I saw this in DevTools as `GET https://shorterloop.com/`.



**5. Server Response**
The server replies with the HTML and a status code. I mostly saw `200 OK`, plus one `304 Not Modified` meaning it was already cached.



**6. Fetching More Files**
While reading the HTML, the browser spots links to CSS/JS files and sends separate requests for each — that's why I saw `testimonials.css`, `common.js`, etc. in the Network tab.



**7. Rendering**
The browser builds the page structure, applies styles, figures out layout, and paints everything on screen.


---



## nslookup Output

```
Command: nslookup shorterloop.com

Server: UnKnown
Address: 10.123.158.129

Non-authoritative answer:
Name: shorterloop.com
Addresses: 64:ff9b::c724:9e64
           199.36.158.100

Command: dig shorterloop.com +short
(dig not available on Windows CMD)
```


---

## Network Tab Requests — shorterloop.com

### Request 1
- **URL:** https://shorterloop.com/assets/css/testimonials.css
- **Status:** 200 OK (from memory cache)
- **Type:** stylesheet
- **Header:** `referrer-policy: strict-origin-when-cross-origin`

`network-tab-1.png`

<img width="700" height="350" alt="Screenshot 2026-06-24 165006" src="https://github.com/user-attachments/assets/68968ecb-173c-4d0f-99a6-e1c495cbea53" />




### Request 2
- **URL:** https://shorterloop.com/assets/scripts/common.js
- **Status:** 200 OK (from memory cache)
- **Type:** script
- **Header:** `referrer-policy: strict-origin-when-cross-origin`


`network-tab-2.png`

<img width="700" height="367" alt="Screenshot 2026-06-24 164947" src="https://github.com/user-attachments/assets/87f3e235-d69d-48ec-9020-379579fedf5d" />

### Request 3
- **URL:** https://shorterloop.com/assets/css/fonts.css
- **Status:** 200 OK (from memory cache)
- **Type:** stylesheet
- **Header:** `referrer-policy: strict-origin-when-cross-origin`

`network-tab-3.png`

<img width="700" height="332" alt="Screenshot 2026-06-24 164924" src="https://github.com/user-attachments/assets/e80d89c2-2b3c-4418-b818-a361e0982487" />



### Request 4
- **URL:** https://shorterloop.com/
- **Status:** 200 OK
- **Type:** document
- **Header:** `referrer-policy: strict-origin-when-cross-origin`


`network-tab-4.png`

<img width="700" height="345" alt="Screenshot 2026-06-24 164901" src="https://github.com/user-attachments/assets/b18ec18a-b02a-410e-914f-5e924c1e9ff5" />



---

## Screenshots
`terminal-nslookup.png`
<img width="400" height="517" alt="Screenshot 2026-06-24 164517" src="https://github.com/user-attachments/assets/a0444f97-4d46-4a8e-9598-0d6872e48bf3" />

`network-tab.png`
<img width="700" height="332" alt="Screenshot 2026-06-24 165054" src="https://github.com/user-attachments/assets/811110ed-49b6-41d6-b676-a1b6e87c80fa" />