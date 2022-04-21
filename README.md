# Multimedia-Adaptive-bitrate-streaming-webserver

# Project Description:
This project stream a stored video using HTTP protocol. To complete the project do the following:
1. Download three videos from the internet or use any other sources to get the videos. The videos
should be of different resolutions.
2. Setup a webserver server on a server using docker containers. You will be given an account on a
server dedicated for this project. You should refrain to use it for any other purpose.
3. Create a Hello webpage (blank webpage with Hello text) on the server,
4. Use port forwarding on the server (docker container) and in the ssh command to test the server
and view the Hello webpage locally (at localhost or 127.0.0.1),
5. For each video in point 1, follow the guidelines for Smart encoding of uploaded videos for adaptive
bitrate streaming of Microsoft (https://docs.microsoft.com/en-us/stream/network-overview) to do
the following:
a. Use ffmpeg to process the downloaded video to generate videos with different qualities,
b. Use ffmpeg to process the downloaded video to generate videos with different resolutions,
6. Use the MP4Box software tool to produce DASH compatible video stream; manifest (.mpd) and
video files (.m4s) and store these files in the root directory of the webserver,
7. Create a main webpage that have links for three video stream webpages. In each of the video
stream webpages add the JavaScript player as shown in the lecture slides.
8. Use any internet browser to view the three webpages locally and play the video.
9. To validate how your web pages load and stream video in poor network connections
a. Perform network throttling in your browser to simulate poor network and view in the
downloaded video chunks
b. Use any webpage testing platform such as BrowserStak to simulate network conditions on
mobile devices.

# Command use:

Run Docker :
command : dokcer run 


find docker ID:
docker ps | grep 1171944

Delete:
rm -r website 
docker kill id then docker rm id

create file first:
mkdir website
touch index.html

create docker:
docker run -dit --name encs5398-ns1171944 -p 8037:80 -v /home/ns1171944/website/:/usr/local/apache2/htdocs/ httpd:2.4


Qualities & Resolution:
ffmpeg -i input.mp4 -c:v libx264 -keyint_min X -g X -an -vf scale=1920:1080 -b:v 3000k video_1080.mp4
X=frames in sec

Sound:
ffmpeg -i Nobody.mp4 -vn -acodec aac my_audio.m4a


Final MP4Box Work:

./MP4Box -dash 1000 -frag 1000 -rap -segment-name 'segment_$RepresentationID$_' -fps 29.97 video1_10_144.mp4#video video1_20_144.mp4#video video1_30_144.mp4#video video1_40_144.mp4#video video1_50_144.mp4#video video1_10_240.mp4#video video1_20_240.mp4#video video1_30_240.mp4#video video1_40_240.mp4#video video1_50_240.mp4#video video1_10_360.mp4#video video1_20_360.mp4#video video1_30_360.mp4#video video1_40_360.mp4#video video1_50_360.mp4#video video1_10_480.mp4#video video1_20_480.mp4#video video1_30_480.mp4#video video1_40_480.mp4#video video1_50_480.mp4#video video1_10_720.mp4#video video1_20_720.mp4#video video1_30_720.mp4#video video1_40_720.mp4#video video1_50_720.mp4#video video1_10_1080.mp4#video:role=main video1_20_1080.mp4#video video1_30_1080.mp4#video video1_40_1080.mp4#video video1_50_1080.mp4#video   audio1.m4a#audio:id=Sound:role=main -out Mainfest/video-manifest.mpd


upolde in server:
pscp -P (port number) project.zip (your name and path on server like: ns1xx9@1xx.1xx.2x4.x85:/home/ns1xx9/website/



Simple Test:
<!DOCTYPE html>
<html>
    <bode>
        <script src="http://cdn.dashjs.org/latest/dash.all.min.js" ></script>
        <video data-dashjs-player src="test2.mpd" controls></video>
    </bode>
</html>

# Note:
1_ I uplode only two mainfest files to show hot it looks like, and if you try to run the program it work.
2_ you have to download M4BOX tool also PSCP if you want to make a docker image and uploade your file on server.


        
