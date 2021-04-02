# geojson extensions for racing track definition

Since much of the spec can be used in 2D and 3D games, 3D-only elements and attributes are suffixed with `*` so a 2D game can ignore implementing those things.


## 1. main track and pit lanes

These shall be described as `LineString`s.

They carry the additional properties:

- `rt:kind`: either `track` or `pit`
- `rt:cross-sections*`: an array of indices, with the same size as the array of positions. One can replace them by `null` to signal the software should interpolate CSs between positions having `null`.
- `rt:camber*` (optional): an array of camber values. a positive camber makes the right side of the cross section skew upwards, a negative one the left side.
- `rt:height*` (optional): an array of heights from sea level, similar to cross sections. `null` values get interpolated too.
- `rt:width` (optional, for 2D only): array of measurements, defines the width of the track section in meters. Works the same way as `rt:cross-sections`

We assume the direction of these line strings define the direction of the track.


## 2. Checkpoints

These shall be 2-point `LineString`s, cutting the track perpendicularly.

Additional properties:
- `rt:kind`: `checkpoint`
- `rt:drs` (optional): either `detect`, `true` or `false`


## 3. Starting grid

These shall be a `Multipoint`.
The car orientation can be derived from the track direction.
The order they are defined is the pecking position, ie. from best qualification time down to last place. 

Additional properties:
- `rt:kind`: `starting-grid`


## 4. Pit stop

These shall be a `Multipoint`.
The car orientation can be derived from the track direction.

Additional properties:
- `rt:kind`: `pit-stop`


## 5. Cross Sections*

These shall be a `MultiLineString`.

Additional properties:
- `rt:kind`: `cross-sections`

Each `LineString` is a profile in meters, with `0, 0` being the center of the track/pit/decoration.
To use one of these, the element ought o reference the cross section index.


## 6. Track Decorations

These shall be `LineString`s.

A side decoration is an auxiliary structure such as a kerb, rail, wall, tires, fence, etc.
A side-decoration starts aligned with the center of the track and the coords are offsets from that center.
This means, if a road segment s 10 m wide, having a kerb at `5, 0` places it starting at the exact right side of the road.

Additional properties:
- `rt:kind`: `track-decoration`
- `rt:family`: `kerb`, `rail`, `wall`, `tires`, `fence`
- `rt:cross-section*`: index of the cross section to use
- `rt:alignment-from-track` (optional): if defined this is the number of meters from the center of the track the decoration offsets. It's like it's glued to the track (this allows for better geometry parameterization for both 2D and 3D). A bit harder to accomplish, inspired by the similar RTB feature.


## 7. Material patches

These shall be `Polygon`s.

They describe the material of the non-track surface.
In order for the map to capture each material in the location, one can have the material assigned, such as dirt, gravel, grass, cement, etc.

Additional properties:
- `rt:kind`: `terrain-material`
- `rt:family`: `dirt`, `grass`, etc.


## 8. Buildings

These shall be `Polygon`s.
   
Additional properties:
- `rt:kind`: `building`
- `rt:height*`: in meters
- `rt:start-height*` (optional) in meters

The reference height should be sea level too?


## 9. Single Models

These shall be `Point`s or `MultiPoint`s.

Additional attributes:
- `rt:kind`: `model`
- `rt:family`: `tree`, `lamp`, `tire`, etc.
- `rt:rotation` (optional): degrees to rotate the model around it's center, in the vertical axis


## 10. Model batch

These shall be `Polygon`s.

Additional attributes:
- `rt:kind`: `model-batch`
- `rt:family`: `tree`, `lamp`, `tire`, etc.
- `rt:density`: density per square meter.

The idea of model batches is to allow a succinct way of describing a forest, set of tires, etc.


## Other Properties

Nothing prevents the author or the game from adding more details as properties, such as `color`s, `texture`s and other variants. The value of sharing a common structure is that most of the track description is shared, by using the elements and properties define above. We suggest custom additions to be done with prefixed properties `game-named-x:`, that way it becomes clear where the extensions are.




## Elements not mapped (yet?)

- camera positions
