Minimal test of showing HBGB-images in different formats using the Rodent-Assimilated Image Server, which is an IIIF made available by University of Oregon Libraries. See:
https://hub.docker.com/r/uolibraries/rais
https://github.com/uoregon-libraries/rais-image-server/wiki

Start docker container with:
docker compose up -d

Images are then accessible as:
{scheme}://{server}/{prefix}/{identifier}/{region}/{size}/{rotation}/{quality}.{format}

For example:
http://localhost:12415/iiif/GB-0998621.jp2/full/full/0/default.jpg
http://localhost:12415/iiif/GB-0998621.jp2/full/2000,/0/default.jpg
where:
1st 'full' -> full region of image
2nd 'full' -> full size, or: '2000,' -> 2000 px in y-dimension, x scaled proportionately
0 -> no rotation
default.jpeg -> standard colours & jpeg format

You can also get info on original info with e.g.:
http://localhost:12415/iiif/GB-0998621.jp2/info.json

########################################################################################

Alternatively, use with IIIF viewer OpenSeadragon (branch dragon-test)
Start IIF server:
docker compose up -d
Start simple web server:
python3 -m http.server 8000
Go to, e.g.:
http://localhost:8000/viewer.html?image=GB-0591417
