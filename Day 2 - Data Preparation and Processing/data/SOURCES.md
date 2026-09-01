# Day 2 Data Sources

## products.csv

A catalogue of 10000 consumer electronics products, used by the walkthrough to
demonstrate missing values, string parsing, categorical encoding, and features
derived from dates. The columns are a product identifier, a product name, a
price, a stock quantity, a warranty period in years, three dimensions held in
one text field, a manufacturing date, an expiration date, a colour and a size
held in a second text field, and a product rating from 1 to 5.

- **Source:** written for this workshop, and generated rather than recorded.
- **Licence:** the same terms as the rest of this repository, because the file
  was written for it.

The file describes no real product and no value in it was measured, so no
conclusion about consumer electronics can be drawn from it.

## sensors/

Particulate matter readings from eight low-cost sensors in the Skopje area,
covering the whole of January 2024. This is the dataset for the laboratory
exercise.

- **Files:** eight, named `station_<id>.csv`, one per sensor.
- **Rows:** 137223 in total, between 13540 and 18059 per file.
- **Columns:** `timestamp`, `pm10`, and `pm25`. The two particulate readings
  are concentrations in micrograms per cubic metre. The station identifier
  appears only in the file name.
- **Period:** 2024-01-01 00:00:11 to 2024-01-31 23:59:58 UTC.
- **Interval:** a median of roughly two and a half minutes per sensor. The
  spacing is irregular and some sensors stopped reporting for a time.
- **Instrument:** every sensor reports a type of SDS011, which is an optical
  particle counter.
- **Source:** the Sensor.Community archive at
  `https://archive.sensor.community/`, specifically the daily `sds011` files
  for 1 to 31 January 2024.
- **Licence:** Open Data Commons Database Contents License 1.0, which
  Sensor.Community publishes as the licence for the contents of its database.

### How These Files Were Prepared

The daily archive files for each sensor were concatenated in timestamp order,
the `P1` and `P2` columns were renamed to `pm10` and `pm25`, and every other
column was dropped. No reading was added, removed, altered, reordered, or
rounded.

The timestamps were re-encoded, and that is the only transformation applied to
a value. The archive records every instant in UTC. Two of the eight files write
their timestamps in Europe/Skopje local time with an explicit `+01:00` offset,
and the other six write them in UTC with no offset at all. Both forms denote
exactly the same instants, so nothing was moved in time. January contains no
daylight saving transition, so the offset is constant throughout.

## stations.csv

One row per sensor, holding `station_id`, `latitude`, `longitude`, and
`sensor_type`.

- **Source:** the position and the instrument type that the Sensor.Community
  archive records for each of the eight sensors. The coordinates are reproduced
  as recorded and none of them was adjusted.
- **Licence:** Open Data Commons Database Contents License 1.0, as above.

## The File The Notebooks Write

Task 8 of the laboratory exercise writes `city_hourly_pm10.csv` into this
directory. That file is an output rather than an input, so the repository does
not store it, and running the laboratory exercise to the end creates it.

## Network Access

Neither notebook reaches the network. Every file the notebooks read is stored
in this directory.
