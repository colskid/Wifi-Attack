# WiFi Attack w/ Wifite, Aircrack-ng, & Hashcat (In Progress)

![Imgur](https://imgur.com/q3Q24ux.jpg)

Welcome to the **WIFI Attack** project! This repository contains resources and examples for capturing a WiFi password using multiple tools including  `wifite` , `aircrack-ng` , & `Hashcat` within the Kali Linux environment.

## Table of Contents

- [Introduction/Disclaimer](#introduction)
- [Wifite](#wifite)
- [Aircrack-ng](#aircrack-ng)
- [Hashcat](#hashcat)
- [Contributing](#contributing)


## Introduction

In this project, I delve into the wireless attack tools available in Kali Linux with the aim of capturing my neighbor's WiFi password. **With his explicit consent**, I sought to achieve this objective and, subsequently, enhance the security of his network based on the findings.

**Disclaimer:**

*Use this project responsibly and ethically. Unauthorized access to computer systems and networks is illegal and unethical. The tools and resources provided in this repository are intended for educational and ethical purposes only. The maintainers of this project are not responsible for any misuse or unlawful activities conducted with the tools provided. By using this project, you agree to use it in compliance with applicable laws and regulations.*

## Wifite
To get started with the project, I needed to start `wifite` in the terminal.

```sh
sudo wifite --kill
```
- --kill: This command will attempt to stop any ongoing wireless attacks initiated by wifite. Keep in mind that the 
          effectiveness of the --kill option can depend on various factors, and in some cases, it might not instantly 
          terminate all processes.

![Imgur](https://preview.redd.it/68orqswiei9a1.png?width=766&format=png&auto=webp&s=f3f74ce211e58943774642f0aa47ad4c3f72d7fb))


## Aircrack-ng

To capture network traffic using tcpdump, I used the following command:
```sh
sudo tcpdump -i eth0 -n -s 0 -w output.pcap
```

- -i eth0: Specifies the interface to capture traffic from. <br>
- -n: Disables hostname resolution for faster capture. <br>
- -s 0: Captures the entire packet. <br>
- -w output.pcap: Writes the captured traffic to the output.pcap file. <br>

## Hashcat

### Capturing HTTP Traffic <br>
To capture HTTP traffic, I used a filter to target HTTP packets:

```sh
sudo tcpdump -i eth0 -n -s 0 -w http_traffic.pcap port 80
```

### Analyzing DNS Queries <br>
To analyze DNS queries, I filtered for DNS packets:

```sh
sudo tcpdump -i eth0 -n -s 0 -w dns_queries.pcap port 53
```

## Contributing 
Contributions to this project are welcome! If you find any issues or want to enhance the project, feel free to submit a pull request.

