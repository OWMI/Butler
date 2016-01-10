# Butler

<h3>What is it?/h3>
<p>Butler is a voice controlled network that spawns webpages that use web speech api to do voice to text (have to use chrome). It then turns commands into actions. Mostly used with <a href="http://github.com/mingram8/Node-House">Node-House</a> to control the home. Also will do YQL queries to get weather data, news, and anything else you could think of</p>

<h3>How to use it</h3>
<p>To just set it up, you should only need to do a npm install. To use it locally (like a mic attatched to the pi) you either need a raspberry pi 2 with chromium installed, or pocketsphinx installed. Set up a shell script with:</p>

<p>pocketsphinx_continuous -hmm /usr/local/share/pocketsphinx/model/en-us/en-us -lm 5016.lm -dict 5016.dic -ds 2 -topn 2 -maxwpf 5 -samprate 16000/8000/48000 -adcdev plughw:1,0  -inmic yes 2>./unwanted-stuff.log | tee ./Butler/words.log</p> <p>That will trascribe what is said into a words file for node to scrape and use. It requires the most recent pocketsphinx built from their guthub. They didn't used to put data in stdout</p>

<p>Another thing I did was make sure that Butler and poxketsphinx are automatically started on restarts. Use sudo raspi-config to make sure that you are booting to the command line and automatically logging in. I boot to startx after so that I could use chromium. So I added startx to the bottom of my ~/.bashrc. That is important because if you boot straight to the desktop, it ignore .xinitrc, which you need to change. Add 
<p>sleep 20 /startUp.sh</p>
<p>To ~/.xinitrc . If it doesn't exist, just create one. In ~/.startUp.sh I have,</p>
<p>#!/bin/bash
./pock.sh &
cd ~/Butler
node server.js</p>

<p>That should do it. I have <a href="ButlerAssistant">Butler Assistant</a> on other pis, that act as a pocketsphinx relay. 

