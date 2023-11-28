# WiFi Attack w/ Wifite, Aircrack-ng, & Hashcat (In Progress)

![Imgur](https://imgur.com/q3Q24ux.jpg)

Welcome to the **WIFI Attack** project! This repository contains resources and examples for capturing a WiFi password using multiple tools including  `wifite` , `aircrack-ng` , & `Hashcat` within the Kali Linux environment.

## Table of Contents

- [Introduction/Disclaimer](#introduction)
- [Wifite](#wifite)
- [Aircrack-ng](#aircrack-ng)
- [Social-Engineering](#social-engineering)
- [Hashcat](#hashcat)
- [Contributing](#contributing)


## Introduction

In this project, I delve into the wireless attack tools available in Kali Linux with the aim of capturing my neighbor's WiFi password. **WITH HIS EXPLICIT CONSENT**, I sought to achieve this objective and, subsequently, enhance the security of his network based on the findings.

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

While `wifite` couldn't crack the password, we successfully captured a `.pcap` file that will prove useful moving forward.

## Aircrack-ng

![Imgur](https://i.imgur.com/jTdZ3fS.png)

To use a dictionary attack with another wordlist, I used this format in `aircrack-ng`:
```sh
sudo aircrack-ng -w /usr/share/wordlists/rockyou.txt /home/kali/Desktop/mikewifi.cap
```

- -w: specifies the path to a wordlist file
- `/home/kali/Desktop/mikewifi.cap`: This is the path to the capture file (mikewifi.cap) that contains the encrypted Wi-Fi data you want to analyze. <br>

Despite attempting to crack the password using the `rockyou.txt` wordlist and several others, I was unsuccessful. After trying over 15 million passwords, I was unable to gain access to the network. 

## Social-Engineering
![Imgur](https://i.imgur.com/u7jaOib.jpg)
Lets start off with the definition.<br> <br>
*What is social engineering?* <br>

Social engineering is a technique used by attackers to manipulate individuals into divulging confidential information, performing actions, or making decisions that they wouldn't typically do. 


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

