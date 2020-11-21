---
title: 'Residency Reflections: Tamara Kametani'
date: 2019-12-10 13:00:00 Z
categories:
- artist-res
tags: web code
layout: post
thumbnail: "/img/res-reflect2/Kametani_T_04.jpg"
excerpt: Agorama's residency reflection focusing on Tamara Kametani's commission.
  Swayze Effect. By Alejandro Ball.
---

### Chasing the Google Map's Car by Alejandro Ball

## Artist Residency

### The beginning
Tamara had a very clear concept and roadmap for the project she wanted to undertake during her residency time with Agorama. The concept... locate Google Street View recording car and secretly insert herself into Google Map. 

The idea originated from an earlier moment when Tamare was still attending her MA with the Royal Academy of Art (London, UK), where she described a moment when she was walking to class and suddenly realised the famous Google Street View car had passed her. In her curiousity, Tamara explored Google Maps in the location of her interaction to discover that she had in fact been captured serindipitously and now was a permenant main stay of the world's largest digital interactive map. 

![](/img/res-reflect2/tamara-beginning.png)

It was with this experience in mind that Tamara approach the Agorama residency; an attempt to reenact this previous experience through the residency process. 

### Residency's approach 

As for the approach to Tamara's residency, this brough Agorama into a position of researcher and proposing various tools and platforms that could possible help Tamara achieve her vision. 

In our first initial meeting we discussed several options for tracking her progress in searching out the Google Street View car's route, from using GPS tracking devices to platforms where she could document the progress of her project. In the end Tamara settled on using Google's own [My Maps](https://mymaps.google.com), which allows for a user to create their own Google map with landmarks, icon placement and the highlighing of walking and driving routes. 

![](/img/res-reflect2/Kametani_T_01.jpg)

We also pursued other options in the case of Tamara failing to find he Google Street View car through the means of other potential surveillance material. One particular example which was attempted and not used for the final work of art is the [TFL Jam Cam public API database](https://api.tfl.gov.uk/Place/Type/JamCam). 

The final elements, which were enacted for Tamara in her project's endeavour were the create's of a closed Whatsapp group of trusted individuals and a meeting with one of the Google Street View car's managers. In the former case, participants that were invited to the closed Whatsapp group were instructed to keep an eye out for the Google Street View car and to photograph it then share it with the group along with the location of the sighting. 

In the latter action, Agorama were able - through insider connections ;) - to score a meeting with a Google Street View car manager. Due to this sensitive nature this is all that will be said on the matter.

## Processes overview

### TFL Jam Cam API
While not included into the final project, this aspect of the collaboration was incredibly fun to put together for Tamara! Essentially it was agreed with Tamara that I would create a simple program that would repeatedly download cctv footage from TFL's Jam Cam API within a 5 mile radius of Tamara’s Google Street View car search route. 

To provide context into the TFL API... the City of London is known as one of the worlds most surveilled cities in the world, with thousands of cameras scattered across the city. The interesting aspect in all this `Big Borther` business is that these thousands of CCTV cameras are not under the control of a single party, and in the case of the CCTV camera attempted to be used for Tamara's project TFL controls roughly 911 different CCTV `Jam Cams` for traffic surveillance purposes. Thus, it was completely legally to work with this online data set (at least at the time)!

Due to the way that footage is captured for the API, it was necessary to create a scrapping system that would repeatedly query the API data set. The reason for this was because TFL only uploads 5 second video clips of its CCTV footage every 5 mins. Thus, the approach, as seen below, was to sort through the data and discover which cameras were in the 5 mile radius that Tamara required. From there is the dataset matches our location criteria, we package the data we want into a json object. From this point the next step is to create a `fetch()` request to the server we want to send the data files to.

_PLEASE NOTE: to attempt this your are required to have a working server that you control with this required storage space and API receiver system inside that server_

At this point all we need to do is create this simple scrapping function into an interval function (meanign a function that runs periodically using the `setinterval()` js function), and tada! You have a CCTV scrapping system that will bestow you with a huge data dump of Jam Cam footage.


```js
        var camObj;
        function jamcall(ev) {
          ev.preventDefault();

          fetch('https://api.tfl.gov.uk/Place/Type/JamCam')
          .then(function(response) {
            return response.json();
          })
          .then(function(myJson) {
            console.log(myJson.length);
            for (var i = 0; i < myJson.length; i++) {
              if (myJson[i].lat > 51.4228 && myJson[i].lat < 51.5967 && myJson[i].lon > -0.3891 && myJson[i].lon < 0.1531) {
                console.log(JSON.stringify(myJson[i].additionalProperties[3].value));
                console.log(JSON.stringify(myJson[i].additionalProperties[2].value));
                console.log(JSON.stringify(myJson[i].additionalProperties[2].modified));

                camObj = JSON.stringify({
                  "name": myJson[i].additionalProperties[3].value,
                  "media": myJson[i].additionalProperties[2].value
                });

                console.log(camObj);

                fetch('http://target.API.receiver/', {
                  method: 'POST',
                  mode: 'cors',
                  credentials: 'omit',
                  header: {'Content-Type': 'application/json'},
                  body: camObj
                })
                .then((response) => {
                  return response.json();
                })
                .then((resJson) => {
                  console.log(resJson);
                })

              };
            }
          })

          setInterval(() => {
            fetch('https://api.tfl.gov.uk/Place/Type/JamCam')
            .then(function(response) {
              return response.json();
            })
            .then(function(myJson) {
              console.log(myJson.length);
              for (var i = 0; i < myJson.length; i++) {
                if (myJson[i].lat > 51.4228 && myJson[i].lat < 51.5967 && myJson[i].lon > -0.3891 && myJson[i].lon < 0.1531) {
                  console.log(JSON.stringify(myJson[i].additionalProperties[3].value));
                  console.log(JSON.stringify(myJson[i].additionalProperties[2].value));
                  console.log(JSON.stringify(myJson[i].additionalProperties[2].modified));

                  camObj = JSON.stringify({
                    "name": myJson[i].additionalProperties[3].value,
                    "media": myJson[i].additionalProperties[2].value
                  });

                  console.log(camObj);

                  fetch('http://target.API.receiver/', {
                    method: 'POST',
                    mode: 'cors',
                    credentials: 'omit',
                    header: {'Content-Type': 'application/json'},
                    body: camObj
                  })
                  .then((response) => {
                    return response.json();
                  })
                  .then((resJson) => {
                    console.log(resJson);
                  })

                };
              }
            })
          }, 300000);

        };

```
If you would like to see that actual data dump of this process, please follow this link: [Agorama TfL datadump](http://cctv-dump.agorama.org.uk/).
Currently, we only have on display the actual day that Tamara request this program to be used. 

### Closed Whatsapp Google Street View car search group (Gallery)

![](/img/res-reflect2/Whatsapp-grp-1.png)
![](/img/res-reflect2/Whatsapp-grp-2.png)
![](/img/res-reflect2/Whatsapp-grp-3.png)
![](/img/res-reflect2/Whatsapp-grp-5.png)
![](/img/res-reflect2/Whatsapp-grp-4.png)

### Tamara Kametani's My Google Map

<iframe src="https://www.google.com/maps/d/embed?mid=1rFaSi2vcBy80ss-csdHdD8Kx9hUYFsGO" width="640" height="480"></iframe>
