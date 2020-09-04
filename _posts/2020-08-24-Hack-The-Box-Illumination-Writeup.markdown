---
layout: post
title: "HTB Illumination Memory Forensics Challenge Write-Up"
date:   2020-08-24 10:30:00 +0100
categories: ["HackTheBox", "Memory Forensics"]
---

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.6/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.6/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

# Stages

1. Download and extract ZIP archive
2. Check master git logs
3. Checkout to commit
4. Get token from config.json
5. Store token in file
6. Use base64 command to decode and retrieve flag

<pre>
<code class="c">
//Discord.JS
const Discord = require("discord.js");
const client = new Discord.Client();
const fs = require("fs");
var config = JSON.parse(fs.readFileSync("./config.json"));


//Node-Hue-API
var hue = require("node-hue-api"),
	HueApi = hue.HueApi,
	lightState = hue.lightState;

//Display command results in console
var displayResult = function(result) {

	console.log(JSON.stringify(result, null, 2));
	
};

//Function taken from campushippo.com
var rgbToHex = function (rgb) { 

  var hex = Number(rgb).toString(16);
  if (hex.length < 2) {

       hex = "0" + hex;
  }

  return hex;
};

//Function taken from campushippo.com
var fullColorHex = function(r,g,b) {   
  var header = "0x"
  var red = rgbToHex(r);
  var green = rgbToHex(g);
  var blue = rgbToHex(b);
  return header+red+green+blue;
};

//Declarations
var host = config.host,
	username = config.username,
	api = new HueApi(host, username),
	state = lightState.create(),
	prefix = config.prefix,
	lightNum = config.lightNum;

//Bot code
client.on("ready", () => {
	console.log(`Logged in as ${client.user.tag}!`);
});

client.on("message", message => {
	if (message.author.bot) return; //Ignore bot messages
	if (message.content.indexOf(prefix) !== 0) return; //Ensure prefix is at the beginning

	const args = message.content.slice(prefix.length).trim().split(/ +/g); //Split command into arguments
	const command = args.shift().toLowerCase(); 

	switch (command) {

		case "light.off" : //Turn light off
			api.setLightState(lightNum, state.off())
		       .then(displayResult)
		       .done();
			message.channel.send("Light Off!");
			break;

		case "light.on" : //Turn light on
			api.setLightState(lightNum, state.on())
			   .then(displayResult)
			   .done();
			message.channel.send("Light On!");
			break;

		case "light.rgb" : //Change light colour
			let r = args[0];
			let g = args[1];
			let b = args[2];
			api.setLightState(lightNum, state.on().rgb(r, g, b))
			   .then(displayResult)
			   .done();
			const embed = new Discord.RichEmbed()
				.setTitle('Light Colour Change')
				.setColor(fullColorHex(r, g, b))
				.setDescription(`Red Value: ${r}. Green Value: ${g}. Blue Value: ${b}`);
			message.channel.send(embed);
			break;

		case "light.switch" : //Switch to different light
			let num = args[0];
			lightNum = num;
			//fs.writeFile("./config.json", JSON.stringify(config))
			message.channel.send(`Light Number switched to ${lightNum}`);
	}
});

client.login(Buffer.from(config.token, 'base64').toString('ascii')) //Login with secret token
</code>
</pre>


<pre>
<code class="c">
{

	"token": "Replace me with token when in use! Security Risk!",
	"prefix": "~",
	"lightNum": "1337",
	"username": "UmVkIEhlcnJpbmcsIHJlYWQgdGhlIEpTIGNhcmVmdWxseQ==",
	"host": "127.0.0.1"

}
</code>
</pre>

{:refdef style="text-align: center;"}
![logs]({{ site.url }}/personal-website/assets/HTB-writeups/Illumination/git-master-logs.PNG)
{:refdef}

{:refdef style="text-align: center;"}
![checkout-to-commit]({{ site.url }}/personal-website/assets/HTB-writeups/Illumination/checkout-to-commit.PNG)
{:refdef}

{:refdef style="text-align: center;"}
![token-file]({{ site.url }}/personal-website/assets/HTB-writeups/Illumination/token-file.PNG)
{:refdef}

{:refdef style="text-align: center;"}
![htb-flag]({{ site.url }}/personal-website/assets/HTB-writeups/Illumination/htb-flag.PNG)
{:refdef}
