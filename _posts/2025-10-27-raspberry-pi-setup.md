---
layout: post
title: My Raspberry Pi 5 Setup
date: 2025-10-27
description: Overview of RPi5 setup for AI/ML usecases
tags: raspberry-pi ml ai hardware
categories: sample-posts
---

Over the past couple weeks, I’ve been putting together a Raspberry Pi 5 setup tailored for **machine learning** and **AI experiments** — a small but capable device that’s going to be the heart of my edge AI projects, and a playground for hybrid cloud-local workflows and deployment experiments.

---

### Why the Raspberry Pi 5

The **Raspberry Pi 5** is a big leap forward compared to its predecessors. It’s built around a **2.4GHz quad-core 64-bit Arm Cortex-A76 CPU**, with **up to 16GB of LPDDR4X RAM**, and most importantly for my use case, support for **PCIe Gen 2 storage** through a dedicated connector.

That PCIe lane unlocks the ability to connect an **NVMe SSD**, which is a game changer for ML workflows. Training models and handling datasets on the Pi 4 often meant crawling speeds due to I/O bottlenecks. The Pi 5 is finally fast enough to be practical for small-scale model training, inferencing, and on-device experimentation.

---

### My Setup

After comparing a few options, here’s the configuration I settled on:

- **Raspberry Pi 5 (16GB RAM)** — the extra memory is essential for heavier Python environments, especially when running TensorFlow, PyTorch, or LLM fine-tuning scripts.
- **Pimoroni NVMe Base** — connects via the new PCIe slot and allows mounting an NVMe SSD for extremely fast read/write performance. The primary reason I went for the Pimoroni NVMe Base over some of the official HATs (Hardware Attached on Top) was the superior thermal management and physical arrangement for active cooling accessories. Unlike the HATs, the Pimoroni NVMe Base is designed to mount the drive beneath the RPi5 board. This keeps the top of the board completely clear and prevents airflow obstruction to the CPU's primary cooling path (less trapped heat prevents thermal throttling under larger training loads).
- **1TB NVMe SSD** — chosen to comfortably store models, datasets, and local project environments without worrying about space. In a scenario where 1TB runs short, I will opt for archiving datasets and older model objects in a cold cloud storage solution such as Google Cloud Storage as retrieval will likely be infrequent.
- **Official Raspberry Pi Active Cooler** — essential to keep temperatures stable during long training sessions, as the Pi 5 runs noticeably hotter than earlier models. One thing I missed was that the official Raspberry Pi case already comes with a cooling fan and a mini heatsink. Due to it being less effective that the active cooler, I opted for removing the pre-installed fan from the case as it is not possible to shut the top cover lid otherwise.
- **Official 27W USB-C Power Supply** — delivers consistent power for the Pi and attached storage under load.
- **Official Raspberry Pi microSD Card (32GB)** — primarily used for the OS boot partition and system files. One thing to note is that this microSD comes with the Debian-based Raspberry Pi OS pre-installed. This is the 32-bit version to ensure maximum backward compatibility. If you would prefer to flash the OS manually on a blank microSD card, the Raspberry Pi Imager software enables downloading the OS image, formatting the card, and partitioning it correctly. The Pi will then boot using the OS you configured.
- **Raspberry Pi Camera Module 3** — a high-quality 12MP camera with autofocus, perfect for **object detection** and **computer vision** projects. It connects via the CSI ribbon cable to the Pi 5’s camera port and offers surprisingly crisp image capture, ideal for training and testing models locally. The camera comes with a CSI ribbon included, no need to purchase one separately.
- **Portable Monitor (HDMI)** — A monitor is not strictly necessary for interacting with a Pi - you can SSH into it and use it headless. But since I was travelling, I was already on the market for a portable monitor to connect to my Mac for split screen coding. I went for a single screen [COOLHOOD 15.6" Portable Monitor](https://www.amazon.co.uk/dp/B0CZNWKV25?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1) from Amazon UK. One thing to note if you're looking for a portable monitor to connect your Pi to is that many portable monitors use a mini-HDMI input post as opposed to standard, full-size HDMI. If you've purchased your Pi with a "Starter Kit", this will likely come with an official micro-HDMI to HDMI cable. This will not work with most portable monitors, so I had to purchase an additional micro-HDMI to mini-HDMI cable to accept video input from the Pi's micro-HDMI port. If you prefer a dual-display setup, the RPi5 comes with two micro-HDMI ports so you can connect to two separate 4K monitors simultaneously.

---

### Storage Strategy

The **microSD card** handles the operating system (Raspberry Pi OS 32-bit), while the **NVMe SSD** serves as the main workspace for my AI projects — storing datasets, Python environments, and outputs.  
As a side experiment, I plan to integrate **Google Cloud Storage (GCS)** to learn how to stream datasets between the cloud and the Pi, simulating a hybrid compute setup.

---

Each experiment will be documented here, with links to the corresponding code and notebooks in my [rasp-pi-projects](https://github.com/arinagn/rasp-pi-projects) repository.

---

### Final Thoughts

This project is as much about **learning the systems side of ML engineering** — storage, optimization, edge computing — as it is about building models.  
If you’re curious about small-scale AI setups or hybrid ML workflows, stay tuned — this is just the beginning.

---

_Next up: SSHing into the RPi5 from a Mac, configuring the NVMe base, and moving the OS filesystem from the microSD card to the NVMe SSD._
