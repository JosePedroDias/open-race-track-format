# geojson extensions for racing track definition

Since much of the spec can be used in 2D and 3D games, 3D-only elements and attributes are suffixed with `*` so a 2D game can ignore implementing those things.


## 1. main track and pit lanes

These shall be described as `LineString`s.

They carry the additional properties:

- `rt:kind`: either `track` or `pit`
- `rt:width`: the default width of the track, in meters.
- `rt:camber*` (optional): the default camber value. a positive camber makes the right side of the cross section skew upwards, a negative one the left side.
- `rt:height*` (optional): the default height of the track, in meters.
- `rt:cross-section*` (optional): the default cross section index to apply to the track. See cross sections.

We assume the direction of these line strings define the direction of the track.


## 2. Key points

These are `Point`s, of the track.

Additional properties:
- `raceway`: `start-finish` or both `start` and `finish`, to identify where the lap gets counted
- `rt:starting-grid`: either `start` or `finish`
- `rt:pit-stop`: either `start` or `finish`
- `rt:drs` (optional): either `detect`, `start` or `finish`
- `rt:sector` (optional): a section number
- `rt:width` (optional): override the default width of the track at this point
- `rt:camber*` (optional): override the default camber of the track at this point
- `rt:height*` (optional): override the default height of the track at this point

## 3. Cross Sections*

These shall be a `MultiLineString`.

Additional properties:
- `rt:kind`: `cross-sections`

Each `LineString` is a profile in meters, with `0, 0` being the center of the track/pit/decoration.
To use one of these, the element ought to reference the cross section index.


## 4. Track Decorations

These shall be `LineString`s.

A side decoration is an auxiliary structure such as a kerb, rail, wall, tires, fence, etc.
A side-decoration starts aligned with the center of the track and the coords are offsets from that center.
This means, if a road segment s 10 m wide, having a kerb at `5, 0` places it starting at the exact right side of the road.

Additional properties:
- `rt:kind`: `track-decoration`
- `rt:family`: `kerb`, `rail`, `wall`, `tires`, `fence`
- `rt:cross-section*`: index of the cross section to use
- `rt:alignment-from-track` (optional): if defined this is the number of meters from the center of the track the decoration offsets. It's like it's glued to the track (this allows for better geometry parameterization for both 2D and 3D). A bit harder to accomplish, inspired by the similar RTB feature.


## 5. Terrain materials

These shall be `Polygon`s.

They describe the material of the non-track surface.
In order for the map to capture each material in the location, one can have the material assigned, such as dirt, gravel, grass, cement, etc.

Additional properties:
- `rt:kind`: `terrain-material`
- `rt:family`: `dirt`, `grass`, etc.


## 6. Buildings

These shall be `Polygon`s.
   
Additional properties:
- `rt:kind`: `building`
- `rt:height*`: in meters
- `rt:start-height*` (optional) in meters

The reference height should be sea level too?


## 7. Single Models

These shall be `Point`s or `MultiPoint`s.

Additional attributes:
- `rt:kind`: `model`
- `rt:family`: `tree`, `lamp`, `tire`, etc.
- `rt:rotation` (optional): degrees to rotate the model around it's center, in the vertical axis


## 8. Model batch

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
