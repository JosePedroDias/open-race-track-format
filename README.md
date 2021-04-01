# Open Race Track Format

## Goal

The objective of this repository is to define a simple enough format that can be used to generate and maintain race tracks. It's supposed to support basic top-down track information but extend also to add 3D information, as will be explained later.
It makes no sense to me that there is no de facto format to start a track from. Games can diverge later by generating dedicated representations for the tracks, but I see value in starting from something that captures the most relevant information about a track. Additionally, this format can also be fed to the game's AI as is.

## The spec

Go read the [spec](race.track.geojson.md).

## Inspiration

Having been a racing game enthusiast I've played and analyzed several tools to author race tracks. Some of them are super easy (such as the one for [gene rally](https://gene-rally.com/)), other super powerful such as [race track builder](http://www.racetrackbuilder.com).

Loving GIS and maps, I have also capitalized on my knowledge of [open street map](https://www.openstreetmap.org/) and it's much simpler cousin GeoJSON [1](https://en.wikipedia.org/wiki/GeoJSON) [2](https://tools.ietf.org/html/rfc7946).

Some example editing sessions:

- [in gene rally](https://www.youtube.com/watch?v=1EUYiNHMu6o&t=4097s). Other games such as 1nsane had a similar approach, by allowing drawing a height map and a set of POIs.
- [in race track builder](https://www.youtube.com/watch?v=ltx2MQ2oBsE)
- [in blender](https://www.youtube.com/channel/UCLHAkKQxzSsa8ltwhMjxE_Q)
- i've also tried to do [torcs/speed dreams](https://en.wikipedia.org/wiki/Speed_Dreams) tracks before by [trying to replicate the trackgen format](https://github.com/JosePedroDias/torcs-track-editor).

Some tracks defined in GeoJSON:
- https://github.com/bacinger/f1-circuits
(these were seminal to this idea)
