it is usual to sometimes ubuntu can't play a specific format from audio files or video files . there is no problem with Rhythmbox or other players , but you have to install a bunch of libraries for your ubuntu desktop .

# Gstream library

it is a powerful library for supporting audio and video files formats . some of its components are installed by default but for more support you need to install all its parts . this is [reference link](https://gstreamer.freedesktop.org/documentation/installing/on-linux.html?gi-language=c) . but if you have not time this is for you :

```shell
sudo apt install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
```
















