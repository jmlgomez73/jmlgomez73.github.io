---
layout: single
title: '<span class="projects">Go Ports - Project</span>'
excerpt: "A fast, concurrent and multithread TCP port scanner."
date: 2021-07-03
categories:
  - projects
tags:  
  - golang
  - scanner
  - reconnaissance
  - threading
show_time: true
---

A fast, concurrent and multithread TCP port scanner.

## [Link to the Github repository](https://github.com/jmlgomez73/GoPorts)

## Installation

* Install Golang in Linux

  ```bash
  sudo apt-get install golang
  ```

  Install Golang in Windows  => [Download Golang](https://golang.org/dl/)

* Clone the repository into your machine

  ```bash
  git clone https://github.com/jmlgomez73/GoPorts
  ```

* Move to the GoPorts directory
  ```bash
  cd GoPorts
  ```
* Check usage and flags, then run your custom command !!
  ```bash
  go run goports -h
  ```

## Flags

| Flag | Description |
|-----|---|
| `-host` | Host or IP address to scan (default "127.0.0.1") |
| `-ports` | Port range to be tested (Ex: 80,443,1-65535,1000-2000) (default "1-65535")  |
| `-threads` | Number of threads to be used (default 900)  |
| `-timeout` | Connection timeout in seconds (default 1s)  |
| `-top20`   | Scanner top 20 most scanned TCP ports  |
| `-top200`  | Scanner top 200 most scanned TCP ports  |


## Usage

Scan the 65535 ports over localhost (127.0.0.1)
  ```bash
  go run goports
  ```
Scan specific ports (21,22,23,80,443) over a specific host (10.10.10.10)
  ```bash
  go run goports -host 10.10.10.10 -ports 21-23,80,443
  ```
Scan specific ports over a specific host, setting a timeout of 5 seconds and using 1000 threads
  ```bash
  go run goports -host www.google.com -ports 80,443 -timeout 5 -threads 1000
  ```
Scan the top 20 tcp ports over a specific host using 1000 threads
  ```bash
    go run goports -host www.google.com -top20 -threads 1000
  ```
This command will scan the top 200 tcp ports on the designated host using 1000 threads
  ```bash
    go run goports -host www.google.com -top200 -threads 1000
  ```