# Convert .svs to .dzi and publish as or embed in a web page 
These are the codes we use to:
- Convert .svs to .dzi and publish as or embed in a web page
- Making a digital pathology archive
- deeply inspired by:
  - https://www.linkedin.com/feed/update/urn%3Ali%3Aactivity%3A6879101264504995841/?comme%5B%E2%80%A6%5DEcard%7Efeed-null-9d6747%7Ekxqtjk75%7Epp-null-voyagerOffline
  - https://www.iis.fraunhofer.de/en/ff/sse/health/medical-image-analysis/mikroskopie/micaia.html
- to select a certain area from a .svs file and reduce the file size, one can use [Imagescope](https://www.leicabiosystems.com/digital-pathology/manage/aperio-imagescope/) and its extract region tool.

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

### download `openseadragon`

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

- see `HE.html` 
<summary>
or minimum example in Details
</summary>
<details>

```html
<meta charset="utf-8"/>
<div id="openseadragon1" style="width: 100%; height: 95%;"></div>
<script src="./openseadragon/openseadragon.min.js"></script>
<script type="text/javascript">
 var viewer = OpenSeadragon({
 id: 'openseadragon1',
 prefixUrl : './openseadragon/images/',
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
</script>
```

</details>



---

### embed in a web page

```markdown

- [https://images.patolojiatlasi.com/template/HE.html](https://images.patolojiatlasi.com/template/HE.html)

- See Microscopy with viewer: 

<iframe src="https://images.patolojiatlasi.com/template/HE.html" width="100%" height="400px"></iframe>

```



---

## further configurations

- https://openseadragon.github.io/examples/tilesource-dzi/

- https://openseadragon.github.io/docs/OpenSeadragon.html

