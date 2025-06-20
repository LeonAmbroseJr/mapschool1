import folium
from openlocationcode import openlocationcode as olc

# Define the center of Rapid City, South Dakota
center_lat, center_lon = 44.0805, -103.2310

# Create a folium map centered at Rapid City
map_rapid_city = folium.Map(location=[center_lat, center_lon], zoom_start=13)

# Define a grid of points around the center to generate OLC codes
delta = 0.01  # spacing for grid
num_points = 5  # number of points in each direction from center

for i in range(-num_points, num_points + 1):
    for j in range(-num_points, num_points + 1):
        lat = center_lat + i * delta
        lon = center_lon + j * delta
        code = olc.encode(lat, lon, codeLength=10)
        folium.Marker(
            location=[lat, lon],
            tooltip=f"OLC: {code}",
            icon=folium.Icon(color='green', icon='info-sign')
        ).add_to(map_rapid_city)

# Save the map to an HTML file
map_rapid_city.save("rapid_city_olc_map.html")
