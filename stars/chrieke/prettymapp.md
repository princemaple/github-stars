---
project: prettymapp
stars: 2630
description: 🖼️ Create beautiful maps from OpenStreetMap data in a streamlit webapp
url: https://github.com/chrieke/prettymapp
---

prettymapp 🖼️
==============

**Prettymapp is a webapp and Python package to create beautiful maps from OpenStreetMap data**

* * *

### 🎈 Try it out here: prettymapp on streamlit 🎈

* * *

  

Based on the prettymaps project
-------------------------------

Prettymapp is based on a rewrite of the fantastic prettymaps project by @marceloprates. All credit for the original idea, designs and implementation go to him. The prettymapp rewrite focuses on speed and adapted configuration to interface with the webapp. It drops more complex configuration options in favour of improved speed, reduced code complexity and simplified configuration interfaces. It is partially tested and adds a streamlit webapp component.

Running the app locally
-----------------------

You can use the webapp directly under prettymapp.streamlit.app or run it locally via:

git clone https://github.com/chrieke/prettymapp.git
cd prettymapp
pip install -r streamlit-prettymapp/requirements.txt
streamlit run streamlit-prettymapp/app.py

Python package
--------------

You can also use prettymapp without the webapp, directly in Python. This lets you customize the functionality or build your own application.

**Installation:**

pip install prettymapp

**Define the area, download and plot the OSM data:**

You can select from 4 predefined styles: `Peach`, `Auburn`, `Citrus` and `Flannel`.

from prettymapp.geo import get\_aoi
from prettymapp.osm import get\_osm\_geometries
from prettymapp.plotting import Plot
from prettymapp.settings import STYLES

aoi \= get\_aoi(address\="Praça Ferreira do Amaral, Macau", radius\=1100, rectangular\=False)
df \= get\_osm\_geometries(aoi\=aoi)

fig \= Plot(
    df\=df,
    aoi\_bounds\=aoi.bounds,
    draw\_settings\=STYLES\["Peach"\],
).plot\_all()

fig.savefig("map.jpg")

You can also plot exported OSM XML files e.g. from openstreetmap.org:

from prettymapp.osm import get\_osm\_geometries\_from\_xml

df \= get\_osm\_geometries\_from\_xml(filepath\="Berlin.osm")
aoi\_bounds \= df.total\_bounds
...

**Customize styles & layers**

Edit the `draw_settings` input to create your own custom styles! The map layout can be further customized with the additional arguments of the `Plot` class (e.g. `shape`, `contour_width` etc.). Check the webapp examples for inspiration.

from prettymapp.settings import STYLES

custom\_style \= STYLES\["Peach"\].copy()
custom\_style\["urban"\] \= {
    "cmap": \["#3452eb"\],
    "ec": "#E9724C",
    "lw": 0.2,
    "zorder": 4,
}

fig \= Plot(
    df\=df,
    aoi\_bounds\=aoi.bounds,
    draw\_settings\=custom\_style,
    shape\="circle",
    contour\_width\=0,
).plot\_all()

You can also customize the selection of OSM landcover classes that should be displayed! Customize the default settings or create your own dictionary! See settings.py for the defaults.

from prettymapp.settings import LANDCOVER\_CLASSES

custom\_lc\_classes \= LANDCOVER\_CLASSES.copy()
custom\_lc\_classes\["urban"\]\["building"\] \= False \# drops all building subclasses
custom\_lc\_classes\["grassland"\]\["leisure"\] \= True \# Include all leisure subclasses
custom\_lc\_classes\["grassland"\]\["natural"\] \= \["island"\] \# Selects only specific natural subclasses

df \= get\_osm\_geometries(aoi\=aoi, landcover\_classes\=custom\_lc\_classes)
