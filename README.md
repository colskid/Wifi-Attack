# WiFi Attack w/ Wifite, Aircrack-ng, & Hashcat (In Progress)

![Imgur](https://imgur.com/q3Q24ux] 

Welcome to the **WIFI Attack** project! This repository contains resources and examples for capturing a WiFi password cracking using multiple tools including  `wifite` , `aircrack-ng` , & `Hashcat` in Kali Linux.

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Examples](#examples)
- [Contributing](#contributing)


## Introduction

In this project, I explore the usage of the `tcpdump` command-line tool to capture network traffic and analyze various protocols and data. This tool is commonly used for troubleshooting network issues, security analysis, and protocol debugging.

## Getting Started

To get started with the project, I needed to have `tcpdump` installed on my system. You can install it using package managers like `apt` or `brew`. Here's how to install it on Ubuntu:

```sh
sudo apt-get update
sudo apt-get install tcpdump
```

## Usage

To capture network traffic using tcpdump, I used the following command:
```sh
sudo tcpdump -i eth0 -n -s 0 -w output.pcap
```

- -i eth0: Specifies the interface to capture traffic from. <br>
- -n: Disables hostname resolution for faster capture. <br>
- -s 0: Captures the entire packet. <br>
- -w output.pcap: Writes the captured traffic to the output.pcap file. <br>

## Examples

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

