# Open Race Track Format

## Goal

Creating race tracks for racing games today is a daunting task, based in proprietary formats and sometimes payed tools.
It makes no sense that there's no de facto format to start a track from. It may even be a starting point, with games diverging later in the arts artifacts pipeline by generating dedicated representations for the tracks with additional details. Still, there's value in starting from something that captures the most relevant information about a track. Another plus is that this format may be suitable as input for game AI to use as is.

The objective of this repository is to define a simple enough format that can be used to design race tracks for racing games to use. It is thought out to capture information suitable for a top-down 2D game but also carries additional optional properties only relevant to 3D games (examples: cross-sections and cambers).

The fact that this is based in GeoJSON brings the benefits that there's already proper tools to edit these such as [JOSM](https://josm.openstreetmap.de/), to render it such as [leaflet](https://leafletjs.com/examples/geojson/) and [even GitHub renders it](examples/portimao.2d.rt.geojson).

## The spec

Here's the [spec](race.track.geojson.md) draft.

This is open for discussion both in the form of issues and suggested changes to the spec via PRs. Would love to know if anyone else adopts this format.

## Inspiration

Having been a racing game enthusiast I've played and analyzed several tools to author race tracks. Some of them are super easy (such as the one for [gene rally](https://gene-rally.com/)), other super powerful such as [race track builder](http://www.racetrackbuilder.com).

Loving GIS and maps, I have also capitalized on my knowledge of [open street map](https://www.openstreetmap.org/) and it's much simpler cousin GeoJSON [1](https://en.wikipedia.org/wiki/GeoJSON) [2](https://tools.ietf.org/html/rfc7946).

Some editing sessions with existing software:

- in [gene rally](https://www.youtube.com/watch?v=1EUYiNHMu6o&t=4097s). Other games such as 1nsane had a similar approach, by allowing drawing a height map and a set of POIs.
- in [race track builder](https://www.youtube.com/watch?v=ltx2MQ2oBsE)
- in [blender](https://www.youtube.com/channel/UCLHAkKQxzSsa8ltwhMjxE_Q)
- I've also tried to do [torcs/speed dreams](https://en.wikipedia.org/wiki/Speed_Dreams) tracks before by [trying to replicate the trackgen format](https://github.com/JosePedroDias/torcs-track-editor).

Some tracks defined in GeoJSON:
- https://github.com/bacinger/f1-circuits
(these were seminal to this idea)
