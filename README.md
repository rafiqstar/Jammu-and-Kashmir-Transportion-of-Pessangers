import phonenumbers
from phonenumbers import geocoder, carrier
from opencage.geocoder import OpenCageGeocode
import folium

# Your API key from OpenCage
key = 'your_opencage_api_key'

# Phone number to track
number = phonenumbers.parse("+919906361392")  # Replace with your phone number

# Get location and carrier information
location = geocoder.description_for_number(number, "en")
service_provider = carrier.name_for_number(number, "en")

# Geocode the location
geocoder = OpenCageGeocode(key)
query = str(location)
results = geocoder.geocode(query)

# Extract latitude and longitude
lat = results[0]['geometry']['lat']
lng = results[0]['geometry']['lng']

# Create a map
my_map = folium.Map(location=[lat, lng], zoom_start=9)
folium.Marker([lat, lng], popup=location).add_to(my_map)

# Save the map to an HTML file
my_map.save("location.html")

print(f"Location: {location}")
print(f"Service Provider: {service_provider}")
print(f"Latitude: {lat}, Longitude: {lng}")
