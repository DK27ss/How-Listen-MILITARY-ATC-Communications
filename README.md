# How-Listen-MILITARY-ATC-Communications

![buckley00](https://github.com/user-attachments/assets/46bb5bd5-1e03-421c-91d3-b7484c28e0e4)

## Overview
I had already been familiar with `ATC` listening and `ADS-B` interception for a little while, but I decided to share this write-up with you.

To put it simply, I will show you how to use the `ATC listening features` of my software, `TYPHOON`, and how to deepen your research using `.asx` and `.pls` listening files provided by the open-source platform `LiveATC`.

![ATC_MAP](https://github.com/user-attachments/assets/84a04197-cdf8-4f7f-88e6-9d68a514137d)

First, I will use TYPHOON to identify various `ICAO codes` with the following color code:

    Blue: Normal
    Orange: Military
    Red: No listening available

By clicking, you can obtain various details about the airport, such as its name, `IATA` and `ICAO codes`, `city`, `type`, `location`, `METAR weather`, as well as the available listening channels and their corresponding frequencies.

![kbkf_datas](https://github.com/user-attachments/assets/5e6a939f-21df-47bb-82fc-e0a8c0f2c14a)

Using the `map overlay` options in TYPHOON, it is also possible to get precise information about the location. (Real-time satellite view coming soon ^^)

![kbkf](https://github.com/user-attachments/assets/ec15e2f2-7714-4db0-9754-caec4a715189)

Normally, when you click on one of the channels for listening, you will be automatically redirected to a `LiveATC link` for live listening through a web app.

However, there are several files `.asx`, `.pls` available that allow direct connection to the `ATC` feed provided by `LiveATC`, and that’s what I’d like to focus on.

![ATC](https://github.com/user-attachments/assets/ecdcca2d-3f5a-40ba-9e92-ba660fb2524c)

If we look inside the `.asx` and `.pls` files, we find interesting information, such as a URL with an `.mp3 file`.

![cat_kbkf](https://github.com/user-attachments/assets/f6366af4-15aa-4386-8c63-5bb7b3e2c5d4)

It is then possible to directly record the transmitted `ATC stream` using `ffmpeg`, a tool for processing audio and video streams.

To do this, use the following command:

    ffmpeg -i http://d.liveatc.net/kbkf1_atis.mp3 capture_kbkf_atis.wav

We can clearly see that it correctly identifies the stream as ATC and also provides the precise name of the channel we are listening to.

You can also use this command for more accurate capture using the provided information, such as the 8000 Hz sample rate:

    ffmpeg -i http://d.liveatc.net/kbkf1_atis.mp3 -ar 8000 -ac 1 -acodec pcm_s16le spectral_capture_kbkf_atis.wav

![listen_kbkf](https://github.com/user-attachments/assets/b5bc6598-c67a-4f42-ad57-dd37e3e58107)

To stop the recording, press `CTRL+C`.

Once your `.wav file` is correctly saved, you can open it and listen to the `captured ATC stream`.

![listen_kbkf_2](https://github.com/user-attachments/assets/8378dc9b-16d7-489b-8376-ae1dd14d8f58)

What's particularly interesting is that we can `reverse-engineer` the captured stream by displaying the `spectrum` at `each frame` of the `.wav file`.
