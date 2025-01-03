---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.16.6
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Garmin GPX

+++

My friend CC shared an output file generated using his Garmin inReach Mini. This files contain GPS locations during trips CC took. I want to
1. Render the points on a map
2. Change the base layer of the map

```{code-cell} ipython3
# install some libraries
!pip install folium gpxpy
```

```{code-cell} ipython3
import folium
import gpxpy
import zipfile
```

## GPX onto a Folium Map

```{code-cell} ipython3
with open('./data/cc-explore.gpx', 'r') as gpx_file:
    gpx = gpxpy.parse(gpx_file)
```

```{code-cell} ipython3
points = []
for track in gpx.tracks:
    for segment in track.segments:
        for point in segment.points:
            points.append([point.latitude, point.longitude])
```

```{code-cell} ipython3
m = folium.Map(location=points[0], zoom_start=10)
```

```{code-cell} ipython3
folium.PolyLine(points, color="red", weight=2.5, opacity=1).add_to(m)
```

```{code-cell} ipython3
m
```

```{code-cell} ipython3

```
