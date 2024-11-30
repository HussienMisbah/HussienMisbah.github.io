---
title: "CyCTF 2024 Finals OSINT Writeups"
header:
  teaser: "/assets/images/osint/logo.png"
tags: ["CTF", "OSINT"]
categories:
  - OSINT
ribbon: yellow
date: 2024-11-30T12:49:18+34:08
toc: true
draft: false
---


CyCTF is organized by [Cyshield](https://www.cyshield.com/)'s cysec team every year , demonstrating new ideas and techniques in different categories (web exploitation , cryptography ,reverse and malware analysis , pwn , OSINT , mobile). it was my pleasure to be the author of SMS and vengeance challenges in web exploitation category and for the OSINT category in qualifcation and finals. this blog post will be about the solutions for the OSINT category in the finals round. My approach for creating the challenges was to not make it sherlock/yandex style ones and to introduce new ideas/techniques that can be used in real life scenarios.

## New Friend

|             |                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------- |
| challenge   | New Friend                                                                                   |
| about       | OSINT process , video analysis , GEOINT , SOCMINT                                                                             |
| description | we have been tracking a female suspect recently and we were able to hack into her mobile phone , however she seems to be very cautious and most likely she already know her phone is not safe anymore , while trying to locate her place it was located in Egypt however we are sure 100% this is not true. we were able to record a short video from her phone before she powered it off eventually and we were not able to identify the location, she has been visiting this places a lot recently, can you help us? an extra information that might be helpful she has been a friend to a multi faceted hairstylist. our goal from this simple task is to reach the hairstylist so we can contact her and get more details about our suspect. the flag is her email address , example flag `CyCTF{fake_staylistmail@gmail.com}`                               |
| attached  | challenge.mp4                                                                        |
| solves | 4  |


Our starting point will be the video given , best approach is to :
- extract all frames from the video to deal with it as images 
- extract audio from the video (to identify language used)

Using online tools like [ezgif](https://ezgif.com/video-to-jpg/) we can extract all frames , the idea of this point is to extract important frames that can help us identify the location. there are 2 important main frames :

First frame , we can identify the following artifacts :
- snow everywhere (we are in winter most likely , this is not the same status always)
- a river (so we are standing on a bridge) 
- stairs in left and right of the river 
- blue lights 
- Tress on left and right 


![image](/assets/images/OSINT/20241116191551.png)

Second Frame :

- Contains 2 big buildings 
- one with blue colors 
- the other one has the word "Terrassen" in it 

![image](/assets/images/OSINT/20241116192114.png)


Doing basic GEOINT on the 2 frames and using google lens on the river frame , will find most images point to sweden , and this frame has same stairs in our frame

![image](/assets/images/OSINT/20241116192445.png)


we can take the image in results and drop it into geospy tool which quickly identifies the location 

![image](/assets/images/OSINT/20241116192715.png)


it is not the most accurate location as from video we are standing on a bridge by a river which matches this location

![image](/assets/images/OSINT/20241116192820.png)


dropping street view we are in same location in video but different weather.

![image](/assets/images/OSINT/20241116192858.png)


Now our goal is to search for the hair stylist/dresser mentioned , form maps there is a hair studio very close to the bridge which we can investigate 

![image](/assets/images/OSINT/20241116193050.png)

![image](/assets/images/OSINT/20241116193123.png)


visiting the place website and in about us page will find team members listed

![image](/assets/images/OSINT/20241116193209.png)


the description mentioned a "Multi-faceted" hairstylist which matches this one called "bero"


![image](/assets/images/OSINT/20241116193248.png)

the page doesn't contain a mail for each person in the team , however a quick search will find the instagram page for the salon and they follow the team members on social media 

![image](/assets/images/OSINT/20241116193405.png)

will find bero's account which contains a link on her bio

![image](/assets/images/OSINT/20241116193434.png)

and finally will find her mail address.

![image](/assets/images/OSINT/20241116193500.png)


## Maybe in another UniVerse

|             |                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------- |
| challenge   | Maybe in another UniVerse                                                                                  |
| about       | osint process  , GEOINT , Metaverse                                                                           |
| description | The Authorities have been tracking a hacker goes with the name "PWner" , he has been travelling from a country to another to erase his steps , he was very cautions recently , he has deleted most of his social media accounts like facebook , instagram and others based on our observations ,so any user with same name you might found most probably a fake one. But recently we were able to find his wife location and she told us the last thing he sent her was this letter , We are sure that she is hiding something although we believe this is the last message from him ,But we can't solve this puzzle , can you help us ? |
| attached  | challenge.png                                                                        |
| solves | 1  |


![image](/assets/images/OSINT/challenge.png)

The idea of challenge is to introduce new area of search which is metaverse assets ,the challenge image gives a big hint with the "another Universe" keyword,also mentioned 2 meta products facebook and instagram , which points to maybe the meta verse ?

Searching for that will find a blog from OSINT Curios which discusses users can create a space and other users can join it so they can talk together and interact with VR in this space.

![image](/assets/images/OSINT/20241105223237.png)

The url format  is `https://www.spatial.io/@jake` we can try add our target instead of `jake` to be `https://www.spatial.io/@PWner`


![image](/assets/images/OSINT/20241105223414.png)


and we have a match , checking his spaces will find one called `1337 Room` , accessing it we can find a cyshield room 


![image](/assets/images/OSINT/20241105223516.png)


Walking through the space will find the flag in an image on the wall 


![image](/assets/images/OSINT/20241105223617.png)



## Complicated

|             |                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------- |
| challenge   | Complicated                                                                                 |
| about       | osint process  , advanced GEOINT , SOCMINT                                                                         |
| description | Hello Old Friend , One of my friends challenged me to solve a case but you have never disappointed me and i don't think you will this time , all we know is that during tracking our target , he have recently attended a football match in France and after that he walked to KFC to have a nice meal, the catch is he made a mistake sharing something that reveals his identity while doing these activities. you may think that you have weak clues to find the target however actually it is not. The flag is the person's name , example "Mohamed Samy" will be CyCTF{Mohamed_Samy} |
| Hint1 | did you know about french territories |
| Hint2 | can you "over pass" ?|
| attached  | none                                                                       |
| solves | 0  |


The challenge description contains several information :
- the search area is France  
- targets went to a stadium to watch a football game 
- the stadium is still active as he was there "recently" 
- he walked to KFC after game meaning the branch is close to the stadium 


So our initial approach is to search for KFCs near stadiums in France , searching this manually will be very time consuming so we can take a smarter approach which is overpass queries , the area is France the target is KFC near stadiums (we can start with 500m) as a start 

```json
[out:json][timeout:25];

area["name"="France"]->.searchArea;


(
  node["leisure"="stadium"](area.searchArea);
  way["leisure"="stadium"](area.searchArea);
  relation["leisure"="stadium"](area.searchArea);
)->.stadiums;


(
  node["amenity"="fast_food"]["name"="KFC"](around.stadiums:500);
  way["amenity"="fast_food"]["name"="KFC"](around.stadiums:500);
  relation["amenity"="fast_food"]["name"="KFC"](around.stadiums:500);
);


out body;
>;
out skel qt;
```
This narrows down possibilities a lot as we can see below 

![image](/assets/images/OSINT/20241110191244.png)

The odd thing we can see in the image is this one , we search "France" and this showed up in results 

![image](/assets/images/OSINT/20241110191611.png)


Searching about that we found the information that france has what is called "Overseas" contains several islands so basically this is french 

![image](/assets/images/OSINT/20241110191530.png)

Zooming in will find the stadium and the KFC Branch

![image](/assets/images/OSINT/20241110191719.png)

Searching for it in google maps

![image](/assets/images/OSINT/20241110191940.png)


Found stadium name is "Stade Roger Zami" , after finding the place the description said he shared something that might reveal his identity , where can we find places and people rather than social media ?

Checking The most famous apps for the location we have found :
- Flicker 
- Instagram 
- Snapmap 

![image](/assets/images/OSINT/20241110192503.png)

![image](/assets/images/OSINT/20241110192559.png)


Finally we found our target and we can confirm it is him by checking comment and description 


![image](/assets/images/OSINT/20241110192616.png)

![image](/assets/images/OSINT/20241110192654.png)


Hope to see you next year !
