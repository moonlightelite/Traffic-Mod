# Traffic-Mod
An MITM traffic modifier for any network traffic

The script uses NFQUEUE + netfilter_queue + scapy to intercept traffic flowing thru a bridge.

More info about netfilter here-
https://home.regit.org/netfilter-en/using-nfqueue-and-libnetfilter_queue/

Requirement-
  Python 2/3
  libnetfilter-queue-dev
  scapy
  (Used on Debian + Ubuntu)

The script was originally written to MITM a popular VPN software in real time. A few years later, for a separate project, I needed to 'convince' some malicious servers that my HTTP client is (amongst other things) of Korean dialicts. This script was modified to change the "Accept-Language:" to "ko-KR" for HTTP traffic.

Steps-
  1. Setup a network bridge (eg. wan eth0 and internal ens38)
  2. Install python3, scapy, and libnetfilter-queue-dev
  3. Modify the iptable rule's --physdev-in to your internal interface (eg. ens38)
  4. Run script with root
  5. Profit!

Questions-
  1. Which popular VPN software are you talking about?
 
  No comment.
  
  2. Does it support HTTPS?
  
  No. Use Burp or https://mitmproxy.org/ for that.
  
  3. The script doesn't work for Python 2!
  
  Meh. The script was originally for Python 2 (it's an old script!)
  
  4. What if I want to add/remove data from TCP packets that changes the length?
  
  It's possible to keeptrack the SYN/ACK numbers to reflect the change, but you'd have to do it yourself.
  
  5. Should I use single thread or multi-queue mode?
  
  Surprisingly single thread has pretty good performance. I got multi-MB/s perforance out of it. I usually set queue # = number of CPU physical cores. You can also add CPU core pinning to the iptable rule for better performance.
