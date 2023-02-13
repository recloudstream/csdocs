---
label: VPN
order: 1000
icon: lock
---
## VPN Types

### Premium
This is the one of the safest options. Like mullvad, surfshark, nord etc. Before purchasing the subscription, please see if the owner of the vpn provider is trustable. For example read [!badge variant="dark" text="this article"](https://www.vpnmentor.com/blog/companies-secretly-own-dozens-vpns/).

### Freemium
These providers give a free tier w/ data cap and very few servers. Like proton`(No data cap)`, windscribe`(10GB/month)`, hide.me`(10GB/month)` etc. But the free servers often have very high ping, low bandwidth and no streaming geo restriction remover.

!!!dark
Windscribe has more free servers than Proton vpn. As a result, you will get less traffic and ping. 
!!!

### Cloudflare WARP

1.1.1.1 is a decent alternative. No data cap. Decent speed. But the problem is you can't choose which server you want use. It'll auto select the server based on your location. You can generate premium account for free which will give you additional benefits.
!!! 1.1.1.1 vs WARP vs WARP+
- 1.1.1.1 provides encrypted DNS.
- WARP provides encrypted DNS, and an encrypted tunnel for all network traffic between your device and the [Cloudflare servers](https://www.cloudflare.com/network/) **nearest to you**.
- WARP+ provides encrypted DNS, and an encrypted tunnel for all network traffic between your device and the Cloudflare servers closest to the website you're accessing. The encrypted traffic is sent through Cloudflare's global private network in a route optimized by Cloudflare's [Argo Smart Routing technology](https://www.cloudflare.com/products/argo-smart-routing/).

	by **u/quinncom**
!!!

!!!secondary You can also read Cloudflare's [!badge variant="dark" text="official documentation about warp modes"](https://developers.cloudflare.com/warp-client/warp-modes/)
!!!

!!!Success Generate free WARP+ data
1. Download [!badge variant="secondary" icon="/static/warp.png" text="1.1.1.1"](https://play.google.com/store/apps/details?id=com.cloudflare.onedotonedotonedotone)
2. Go to [!badge variant="dark" text="1.1.1.1"] → [!badge variant="dark" text="Settings"] → [!badge variant="dark" text="Advanced"] → [!badge variant="dark" text="Diagnostics"]  and copy the [!badge variant="dark" text="ID"]
3. 
	1. [!badge variant="dark" text="Run"] [!badge variant="secondary" text="Replit"](https://replit.com/@aliilapro/warp) and paste your [!badge variant="dark" text="ID"] there.
	2. Or, Go to [!badge variant="secondary" text="Google collab"](https://colab.research.google.com/github/TheCaduceus/WARP-UNLIMITED-ADVANCED/blob/main/ipynb/Colab.ipynb), paste your [!badge variant="dark" text="ID"] there and run the program.

The program will now generate 1GB free WARP+ referral reward after every 20 seconds. You have to wait a bit to see the referral reward in the app.
!!!

### Self Hosted

A self-hosted VPN is a VPN service that is set up and managed by the user, rather than by a third-party VPN provider. This means that the user is responsible for setting up and maintaining the VPN server, as well as for securing the VPN connection.

There are several advantages to using a self-hosted VPN. One is that the user has full control over the VPN server and can configure it to meet their specific needs. Another advantage is that the user can be sure that their internet traffic is not being logged or monitored by a third-party VPN provider.

To set up a self-hosted VPN, the user will need to have a server (physical or virtual) that is connected to the internet and that is configured to run VPN software. There are several different VPN software packages that can be used, such as OpenVPN, WireGuard, and StrongSwan. These software packages can be installed on the server and configured to create a VPN connection.

!!!light Summary
A self-hosted VPN is a VPN service that is set up and managed by the user. It offers the user full control over the VPN server, but also requires a certain level of knowledge and maintenance. It is important to weigh the benefits and drawbacks before deciding to go for a self-hosted VPN.
!!!

!!!info [Sample Tutorial](https://www.youtube.com/watch?v=E-CLtExRzX8)
!!!

!!!danger Avoid these vpn options
1. No mod vpn. If you can mod your vpn, then it's not a good vpn.
2. No ad supported vpn. To provide ad they need data which defeats the main purpose.
3. One time purchase/ full free. Their business model is always questionable
!!!
___

## HTTPS vs DoH vs VPN

**HTTPS (Hypertext Transfer Protocol Secure)** is a protocol for secure communication over the internet. It encrypts the communication between a website and a user's browser to protect against eavesdropping and tampering.

**DoH (DNS over HTTPS)** is a protocol for securely resolving DNS (Domain Name System) queries over HTTPS. It encrypts DNS queries to prevent eavesdropping and tampering, and helps to prevent censorship and other forms of tampering with DNS resolution.

**VPN (Virtual Private Network)** is a technology that creates a secure, encrypted tunnel between a device and a VPN server. This allows users to access the internet as if they were connected to a private network, and can be used to protect against eavesdropping, tampering, and censorship.

!!!light Summary
HTTPS protects the communication between the browser and the website, DOH protects the communication between the client and the DNS server and VPN protect the communication between the device and the internet. They are different protocols with different goals but all of them aims to increase security and privacy.
!!!

___

## Does VPN speed up your connection?

Using a VPN can sometimes impact your internet connection speed, as your internet traffic has to be routed through an encrypted tunnel to a VPN server before it reaches the internet. This extra step can add some latency to your connection, which can result in slower download and upload speeds.

However, in some cases, a VPN can actually improve your video streaming speed. This is because some ISPs (Internet Service Providers) use traffic shaping techniques to limit the bandwidth of certain types of internet traffic, such as video streaming. By using a VPN, you can bypass these limitations and access the internet as if you were connected to a different network.

Additionally, some VPNs offer servers specifically optimized for streaming, allowing you to connect to a server that is closest to the streaming service’s servers, reducing the distance and latency your data has to travel, which can result in faster streaming speeds.

!!!info
It is important to note that the effect of VPN on video streaming speed can be highly dependent on several factors such as the VPN provider, the server location, your internet connection speed, and the distance between your device and the VPN server.
!!!

!!!light Summary
Using a VPN can potentially increase your video streaming speed but it also can decrease it depending on the factors mentioned before. It is recommended to test the VPN connection with and without a VPN to measure the difference in streaming speed.
!!!

___

## VPN and security

When you use a VPN, your internet traffic is routed through an encrypted tunnel to a VPN server before it reaches the internet. This makes it difficult for your ISP (Internet Service Provider) to see which websites you are visiting.

However, it is important to note that while a VPN can make it difficult for your ISP to see which websites you are visiting, it is not impossible. Some VPNs may not provide perfect forward secrecy, which means that if an attacker intercepts your internet traffic, they may be able to decrypt it and see which websites you are visiting. Additionally, some VPNs may keep logs of your internet activity, which could be accessed by your ISP or other third parties.

So, to ensure that your ISP cannot see which websites you are visiting, it is important to use a reputable VPN service that has a good track record of protecting user privacy and not keeping logs. Additionally, using a VPN with perfect forward secrecy and a high level of encryption is a good choice. Or, you can use Self hosted vpn.

!!!light Summary
Using a VPN can make it more difficult for your ISP to see which websites you are visiting, but it is not a guarantee that they won't be able to see it. It is important to use a reputable VPN service that has a good track record of protecting user privacy.
!!!
