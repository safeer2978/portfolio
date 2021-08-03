---
title: "Sunno"
tagline: "A Spotify-like music streaming application backend using microservice architecture"
website: "https://github.com/safeer2978/Sunno-backend
skills: ["Java", "Spring", "Microservice", "JWT", "Eureka", "ZUUL"]
---

 A Spotify-like music streaming application backend using microservice architecture implemented in Spring Boot

This is my attempt to build a media platform to learn microservices in action. This is nowhere close to Spotify though I will try to continue improving/building new features on top of this.

Since this is a microservice architecture, we have the following services

*  **account service**

	* This service manages the user data and Subscriptions. It authenticates the user and grants authorizations and provides access and refresh tokens.

* **view service**

 	* This service provides music data for the user to browse through. the music data includes track, album and artist details along with the track id.

 	* it is also used to Playlist operations like creation, adding tracks, removing tracks, etc.
	
* **play service**

	* This service has the sole purpose to distribute a time-restricted link of the resource(CDN) to the user upon receiving a track id and validating the access token

Besides these, there's an API gateway implemented using Netflix ZUUL and a service registry using Netflix Eureka.

there is also an upload application which runs on the resource owners system, which processes the music files to collect relevant track data, fetches free links to album covers, etc, and pushes the data to view service database for the user to browse and the music file to the AWS S3 bucket.


