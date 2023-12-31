# WiFi Attack w/ Wifite, Aircrack-ng, & Hashcat

![Imgur](https://imgur.com/q3Q24ux.jpg)

Welcome to my **WIFI Attack** project! This repository contains resources and examples for capturing a WiFi password using multiple tools including  `wifite` , `aircrack-ng` , & `hashcat` within the Kali Linux environment.

## Table of Contents

- [Introduction/Disclaimer](#introduction)
- [Wifite](#wifite)
- [Aircrack-ng](#aircrack-ng)
- [Social-Engineering](#social-engineering)
- [Research](#research)
- [Hashcat](#hashcat)
- [Conclusion](#conclusion)
- [Contributing](#contributing)

<br><br>

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

Wifite automates various stages of a wireless network attack, particularly focusing on Wi-Fi networks. The stages of a Wifite attack typically include:

- **Scanning**: Wifite scans the surrounding area for available Wi-Fi networks. It identifies SSIDs, encryption types, signal strengths, and other relevant information.
- **Target Selection**: The user selects the target Wi-Fi network for the attack. Wifite can target specific networks based on the user's input or automatically select the best target based on predefined criteria.
- **Attack Initialization**: Wifite initializes the selected attack based on the chosen options. This may include WEP attacks, WPA/WPA2 dictionary attacks, brute-force attacks, PMKID attacks, or attacks against WPS vulnerabilities.
- **Dictionary Attack (WPA/WPA2)**: If the target network uses WPA or WPA2 encryption, Wifite may perform a dictionary attack. It tries to crack the pre-shared key by systematically testing passwords from a specified wordlist.
- **Bruteforce Attack**: Wifite may conduct a brute-force attack by systematically trying all possible password combinations until the correct one is found. This is often a last resort and can be time-consuming.
- **WEP Attacks**: If the target network uses WEP encryption (which is outdated and insecure), Wifite may perform attacks specific to WEP.It attempts to crack the WEP key using various methods.
- **PMKID Attack (WPA/WPA2)**: Wifite can use the PMKID attack method to crack WPA/WPA2 pre-shared keys without capturing a full handshake.This is a faster method compared to traditional handshake-based attacks.
- **WPS Attacks**: Wifite may conduct attacks against the Wi-Fi Protected Setup (WPS) feature, exploiting vulnerabilities to gain access to the network.
- **Successful Authentication**: If the attack is successful, Wifite informs the user and provides the key or password that was cracked.

![Imgur](https://preview.redd.it/68orqswiei9a1.png?width=766&format=png&auto=webp&s=f3f74ce211e58943774642f0aa47ad4c3f72d7fb)
<br> <br> <br>
While `wifite` couldn't crack the password, we successfully captured a `.cap` file that will prove useful moving forward.

*A `.cap` file, in the context of wireless network security, is commonly associated with Aircrack-ng and other tools used for capturing and analyzing Wi-Fi traffic. It stands for "capture" and is often used to store data related to Wi-Fi handshakes and other network activities.*
<br><br>

## Aircrack-ng

![Imgur](https://i.imgur.com/jTdZ3fS.png)

To use a dictionary attack with another wordlist, I used this format in `aircrack-ng`:
```sh
sudo aircrack-ng -w /usr/share/wordlists/rockyou.txt /home/kali/Desktop/mikewifi.cap
```

- `-w`: specifies the path to a wordlist file
- `/home/kali/Desktop/mikewifi.cap`: This is the path to the capture file (mikewifi.cap) that contains the encrypted Wi-Fi data you want to analyze. <br>

Despite attempting to crack the password using the `rockyou.txt` wordlist and several others, I was unsuccessful. After trying over 15 million passwords, I was still unable to gain access to the network. 
<br><br>

## Social-Engineering

![Imgur](https://i.imgur.com/u7jaOib.jpg)
Lets start off with the definition.<br> <br>
*What is social engineering?* <br>
Social engineering is a technique used by attackers to manipulate individuals into divulging confidential information, performing actions, or making decisions that they wouldn't typically do. <br><br>

**The following day:** I happened to run into my neighbor and recounted my endeavor of attempting over 15 million password combinations to access his WiFi without success. He chuckled at the sheer magnitude of the attempts and casually mentioned that he believed he was still using the default password provided by his internet service provider (ISP). This casual conversation sparked my curiosity. I began pondering whether ISPs follow a specific method in crafting default passwords. Has anyone delved into this inquiry before? The moment had arrived to embark on a journey of exploration and research.
<br><br>

## Research
![Imgur](https://i.imgur.com/9ITPxus.jpg)

After conducting an extensive research dive, a discernible pattern emerged in this ISPs default passwords: a straightforward structure consisting of (first word)(second word)(three-digit number). Delving further into this revelation, I stumbled upon an article revealing that someone had already compiled a list adhering to this format. The list was ingeniously generated by appending adjectives and nouns followed by three digits. However, there was a caveat – the file size amounted to a hefty 90 gigabytes, a space requirement beyond the capacity of my Linux machine.

Undeterred, the creator had also crafted a more manageable wordlist, containing just the words without the digits. This pared-down file offered a significantly reduced size that was usable on my machine. The upcoming section will unravel whether we can successfully crack the password using `hashcat`.

<br><br>

## Hashcat

![Imgur](https://i.imgur.com/6aPbi7F.jpg)

The first thing I had to do was convert the mikewifi.cap to mike.hc22000 using a tool:

```sh
sudo hcxpcapngtool -o mike.hc22000 mikewifi.cap 
```

*The command hcxpcapngtool in the terminal is employed to convert a captured WiFi traffic file, represented in the PCAP-NG format as mikewifi.cap, into the HCCAPX format. The resulting file, named mike.hc22000, is formatted to store critical information related to WiFi handshakes. The HCCAPX format is commonly utilized in tools like Hashcat, particularly for offline password cracking attacks against WiFi handshakes. This conversion process is integral to preparing the captured data for subsequent security analyses and experiments within the project.*

In Hashcat, the numerical value in the file extension, such as the 22000 in mike.hc22000, corresponds to the hash mode. In Hashcat, hash modes define the type of hash algorithm and the specific parameters used for hashing. Each hash mode is associated with a unique numerical identifier.

The `22000` hash mode specifically represents WPA/WPA2 (Wireless Protected Access) hashes with PMKID (Pairwise Master Key Identifier). PMKID is a type of information obtained during a WPA/WPA2 handshake. Hashcat uses different modes for various types of hash algorithms and cryptographic processes.

Now armed with this information, let's explore the possibility of deciphering the password using our newly acquired `mike.hc22000` file.

First, i want to `cd` into the folder where the `mike.hc22000` file is located, mine was on the Desktop. 

```sh
cd Desktop  
```
Then:

```sh
sudo hashcat -m 22000 -a 6 mike.hc22000 /usr/share/wordlists/isp.txt ?d?d?d   
```

Explanation:

- `-m 22000`: Specifies the hash mode, indicating WPA/WPA2 PMKID.
  
- `-a 6`: Specifies the attack mode, set to attack mode 6 (brute-force).

- `mike.hc22000`: Input file containing WPA/WPA2 PMKID hashes.

- `/usr/share/wordlists/isp.txt`: Path to the wordlist file (isp.txt) for the brute-force attack.

- `?d?d?d`: Represents a mask for the brute-force attack, where `?d` denotes a digit, and the pattern `?d?d?d` indicates three digits.

At this point, `hashcat` initiated the process, estimating approximately 2.5 hours to exhaustively explore all possible combinations. Surpassing expectations, within an hour and a half, the password was successfully deciphered, adopting a format of (adjective)(noun)(3 digits).

<br><br>

## Conclusion

The WIFI Attack project delved into the realm of wireless security using tools such as `wifite`, `aircrack-ng`, and `hashcat` within the Kali Linux environment. With explicit consent from my neighbor, the objective was to enhance the security of his network by exploring potential vulnerabilities.

Through the journey:
- **Wifite** automated various stages of wireless network attacks, focusing on Wi-Fi networks. Despite not cracking the password, valuable data in the form of a .pcap file was successfully captured.
- **Aircrack-ng** attempted dictionary attacks using wordlists, revealing the challenge of cracking passwords despite exhaustive attempts.
- **Social Engineering** introduced the concept of manipulating individuals to extract information, prompting a curious exploration into the methods employed by Internet Service Providers in crafting default passwords.
- **Research** uncovered a pattern in ISPs' default passwords, leading to the discovery of a wordlist tailored for such scenarios.
- **Hashcat** played a pivotal role, converting captured data to the HCCAPX format and successfully deciphering the password using a tailored brute-force attack.

In the end, the project not only highlighted the importance of ethical hacking practices but also showcased the need for robust password policies and user awareness. By responsibly employing these tools, we can contribute to a more secure and resilient digital environment.

<br><br>

## Contributing 
Contributions to this project are welcome! If you find any issues or want to enhance the project, feel free to submit a pull request.

