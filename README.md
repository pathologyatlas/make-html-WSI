# Convert .svs to .dzi and publish as or embed in a web page 
- Convert .svs to .dzi and publish as or embed in a web page
- Making a digital pathology archive

## install requirements

### install `VIPS`

- https://www.libvips.org/install.html

```zsh
brew install vips
```

### install `openslide` (seems to be optional)

- https://openslide.org/download/

```zsh
brew install openslide
```

- https://github.com/openslide/openslide-python

```zsh
pip3 install openslide-python
```

### download openseadragon

- https://openseadragon.github.io/

- https://github.com/openseadragon/openseadragon/releases/download/v3.0.0/openseadragon-bin-3.0.0.zip


## have your .svs image in working directory

- https://openseadragon.github.io/examples/creating-zooming-images/

### use vips to convert .svs to .dzi

```zsh
vips dzsave HE.svs HE
```

this runs a long time depending on file size


### which generates
 
- one file: `HE.dzi`

- one folder: `HE_files` This folder contains multilevel images

## open `.dzi` file with a textreader

```
<?xml version="1.0" encoding="UTF-8"?>
<Image xmlns="http://schemas.microsoft.com/deepzoom/2008"
  Format="jpeg"
  Overlap="1"
  TileSize="254"
  >
  <Size 
    Height="30580"
    Width="51792"
  />
</Image>
```

## prepare `HE.html` file to read files in a web page

- https://openseadragon.github.io/docs/


<summary>
- see `HE.html`
</summary>
<details>
```html
<meta charset="utf-8"/>
<div id="openseadragon1" style="width: 100%; height: 95%;"></div>
<script src="./openseadragon/openseadragon.min.js"></script>
<script src="openseadragon/openseadragon-scalebar.js"></script> <!-- for scalebar -->
<script type="text/javascript">
 var viewer = OpenSeadragon({
 id: 'openseadragon1',
 prefixUrl : './openseadragon/images/',
 showHomeControl : false, // optional
 showRotationControl : true,  // optional
 showNavigator : true,  // optional
 showFlipControl: true,  // optional
 navigatorBackground: 'rgb(240, 240, 240)',  // optional
 tileSources: {
 Image: {
Url: './HE_files/', // name of image folder
TileSize: '254', // see .dzi file
Overlap: '1', // see .dzi file
Format: 'jpeg', // see .dzi file
ServerFormat: 'Default', // optional
xmlns: 'http://schemas.microsoft.com/deepzoom/2009', // see .dzi file
Size: {
 Width: '51792', // see .dzi file
 Height: '30580' // see .dzi file
 } 
 }}});
// for scalebar
viewer.scalebar({ 
minWidth: '100px', 
pixelsPerMeter : '1.98255e+06', 
fontFamily : 'Arial', 
backgroundColor : 'rgba(255, 255, 255, 0.5)', 
fontSize : 'small', 
barThickness : '2', 
xOffset : '10', 
yOffset : '10'  
});
</script>
```
</details>



## further configurations

- https://openseadragon.github.io/examples/tilesource-dzi/

- https://openseadragon.github.io/docs/OpenSeadragon.html

