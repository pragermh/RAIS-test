# RAIS-test

Minimal setup for serving large herbarium images via the **Rodent-Assimilated Image Server (RAIS)** — a IIIF ('triple-eye-eff')-compliant server by the University of Oregon Libraries — and viewing them with **OpenSeadragon** for smooth zooming and panning.

## Requirements

- Docker and Docker Compose installed  
- Python 3 (to start a simple web server for `viewer.html`)

## Structure

```
RAIS-test/
├── docker-compose.yml      # Starts the RAIS IIIF server
├── images/                 # Folder with JP2 images
├── README                  # This file
└── viewer.html             # Simple web page with OpenSeadragon viewer
```

## Getting started

1. **Start the RAIS IIIF server**  
   The server loads images from `./images` and makes them available via the IIIF API on port **12415**:
   ```
   docker compose up -d
   ```

2. Start a simple web server in the project folder to serve viewer.html:
   ```
   python3 -m http.server 8000
   ```

3. Open the viewer in your browser:
   ```
   http://localhost:8000/viewer.html?image=GB-0526335
   ```
   Replace GB-0526335 with the filename (without .jp2) of any image in the images folder.

## How the RAIS IIIF server works

Images are accessible via URLs following the IIIF Image API pattern:
```
{scheme}://{server}/{prefix}/{identifier}/{region}/{size}/{rotation}/{quality}.{format}
```
Examples:

Get the full image at full size in JPEG format:
```
http://localhost:12415/iiif/GB-0998621.jp2/full/full/0/default.jpg
```
Get the same image with width 2000 pixels (height scaled proportionally):
```
http://localhost:12415/iiif/GB-0998621.jp2/full/2000,/0/default.jpg
```
Get image metadata:
```
http://localhost:12415/iiif/GB-0998621.jp2/info.json
```

## How OpenSeadragon works

[OpenSeadragon](https://openseadragon.github.io/) is a JavaScript library for viewing large, zoomable images.  
It loads only the visible parts of an image as small tiles, so you can pan and zoom smoothly without downloading the entire file.  
When used with a IIIF server like RAIS, it reads `info.json` to know how to request the right tiles at the right resolution.

See a live OpenSeadragon IIIF demo [here](https://openseadragon.github.io/examples/tilesource-iiif/).
