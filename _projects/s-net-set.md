---
title: "Sunno"
tagline: "A networked multiplayer "
website: "https://github.com/vakila/net-set"
skills: ["JavaScript", "Node", "Express", "Sockets", "Functional Programming", "TDD"]
---

# _Sunno_ - A Spotify-like music streaming application backend using microservice architecture implemented in Spring Boot

This is my attempt to build a media platform to learn microservices in action. This is nowhere close to Spotify though I will try to continue improving/building new features on top of this.

**Detailed documentation is available in README.md in the directory of each service.**

#### Features completed till now: -
- [x] Sign in and User Profile
- [x] Upload Content data and files
- [x] Browse Content
- [x] Create, Add and remove Playlists
- [x] Play Music

#### Features to be added subsequently: -

- [ ] Sign in with Google / Facebook
- [ ] Subscription
- [ ] Search Content
- [ ] Recommend Content
- [ ] Lyrics Content
- [ ] Download Content
- [ ] Group Session


## System Design


* The basic flow from a client perspective is (here the user implies the client application):

	* the user authenticates to get an access token.

	* the user browses the library and chooses a track to play.

	* the user request for a link to the track, offering the track id and the access token.

 	* the user receives a link to track which can then be used for streaming.


	![alt text](https://github.com/safeer2978/Sunno-backend/blob/master/Diagrams/HLD.png)


the entire backend is built using Spring Boot and the Media server is AWS S3 bucket where the media files are stored; these are accessed by the client through a CDN, in this case, AWS Cloudfront.

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

**Detailed documentation is available in README.md in the directory of each service.**

## Usage

This system makes use of AWS S3 and CloudFront CDN for music streaming, however, you may modify it to make use of any other media server.

For each service, there are certain configurations that you may want to change. Instructions for the same are available in the README.md of respective service in respective dir.
