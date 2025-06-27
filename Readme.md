Use tileserver-gl to start the server

and --verbose for debugging

pm2 start npm --name tileserver -- run start

docker-compose logs -f
docker-compose down
docker-compose up -d

use git lfs track "egypt.mbtiles"  to track large files
git rm --cached egypt.mbtiles  to remove them from normal git
git lfs pull to pull them on the server as without this it uses a url ref to the file not the file itself


download .pbf tiles from https://download.geofabrik.de/africa/egypt.html

use   docker run --rm -it \
  -v /mnt/d/Test/MapTiler:/srv \
  tilemaker \
  --input=/srv/egypt-latest.osm.pbf \
  --output=/srv/egypt.mbtiles \
  --config=/srv/config-coastline.json \
  --process=/srv/process-coastline.lua  \
  --bbox=21.80407,18.22647,39.93883,35.79160

to transform it to .mbtiles file

use https://github.com/openmaptiles/maptiler-basic-gl-style?tab=readme-ov-file to get styles and don't forget to replace the tiles, fonts and sprites to use our custom already downloaded data

Deploy steps
- cd tiles-server
- git pull
- git lfs pull  (if you added a new file that is lfs tracked)
- docker-compose down
- docker-compose up -d


you can find the coastline and land cover files at  
- https://osmdata.openstreetmap.de/download/water-polygons-split-4326.zip (For Seas and this is the important one)
- https://naciscdn.org/naturalearth/10m/physical/ne_10m_antarctic_ice_shelves_polys.zip (can be ignored)
- https://naciscdn.org/naturalearth/10m/cultural/ne_10m_urban_areas.zip (can be ignored)
- https://naciscdn.org/naturalearth/10m/physical/ne_10m_glaciated_areas.zip (can be ignored)