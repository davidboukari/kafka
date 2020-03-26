# Python

## requirements.txt

```bash
arrow==0.15.5
attrs==19.3.0
confluent-kafka==1.3.0
importlib-metadata==1.5.0
jsonschema==3.2.0
kafka==1.3.5
kafka-python==2.0.1
pyrsistent==0.16.0
python-dateutil==2.8.1
six==1.14.0
times==0.7
urllib3==1.25.8
zipp==3.1.0
```

## Account creation to get a key

* https://developer.jcdecaux.com/#/signup

## Producer velib-get-stations.py

```bash
import json
import time
import urllib.request

from kafka import KafkaProducer

API_KEY = "XXX" # FIXME Set your own API key here
url = "https://api.jcdecaux.com/vls/v1/stations?apiKey={}".format(API_KEY)

producer = KafkaProducer(bootstrap_servers="localhost:9092")

while True:
    response = urllib.request.urlopen(url)
    stations = json.loads(response.read().decode())
    for station in stations:
        producer.send("velib-stations", json.dumps(station).encode())
    print("{} Produced {} station records".format(time.time(), len(stations)))
    time.sleep(1)
```

## Consumer: velib-monitor-stations.py

```bash
import json
from kafka import KafkaConsumer

stations = {}
consumer = KafkaConsumer("velib-stations", bootstrap_servers='localhost:9092', group_id="velib-monitor-stations")
for message in consumer:
    station = json.loads(message.value.decode())
    station_number = station["number"]
    contract = station["contract_name"]
    available_bike_stands = station["available_bike_stands"]

    if contract not in stations:
        stations[contract] = {}
    city_stations = stations[contract]
    if station_number not in city_stations:
        city_stations[station_number] = available_bike_stands

    count_diff = available_bike_stands - city_stations[station_number]
    if count_diff != 0:
        city_stations[station_number] = available_bike_stands
        print("{}{} {} ({})".format(
            "+" if count_diff > 0 else "",
            count_diff, station["address"], contract
        ))

```
