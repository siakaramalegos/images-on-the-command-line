# Images on the Command Line

A set of tricks for modifying images using various command line tools. I always forget them so I wanted one place to bookmark. :)

Currently all commands are for MacOS/Linux.

For programmatically altering images in a Node application, use [Sharp](https://www.npmjs.com/package/sharp). For individual image processing, I usually reach for [ImageMagick](https://www.imagemagick.org/script/index.php) on the command line. One great resource for both tools is [Serve Responsive Images](https://web.dev/serve-responsive-images) by [Katie Hempenius](https://twitter.com/katiehempenius).

## ImageMagick

**Installation**

On a Mac, to install ImageMagick, use homebrew:

```
$ brew install imagemagick
```

**Usage**

To change file formats:

```
$ convert galaxy.png galaxy.jpg
```


To only resize:

```
$ convert galaxy.jpg -resize 500 galaxy_500.jpg
```

Resize and crop:

```
$ convert original.jpg -resize "500^>" -gravity center -crop 500x500+0+0 -strip cropped.jpg
```

Resize and crop, but can adjust offset of where to crop:

```
$ convert -crop 100x100+50+50 input_image.jpg output_image.jpg
```

Explanation:

- `gravity center` center the next operation
- `+profile "*"` do not save any metainfo to the jpeg (making the resulting image smaller). I think `strip` does this too?

Info from https://superuser.com/questions/275476/square-thumbnails-with-imagemagick-convert

## `cwebp`

[Documentation](https://developers.google.com/speed/webp/docs/cwebp)

**Installation**

On a Mac, to install `cwebp`, use homebrew:

```
$ brew install cwebp
```
For Windows `choco install webp`, Red Hat `yum install libwebp-tools`, Node-based `npm i -g cwebp-bin`

**Usage**

Convert source.png to a lossy webp file output.webp with a quality of 75 (0-100): 

```
$ cwebp -q 75 source.png -o output.webp
```

Convert source.png to a lossless webp file output.webp: 

```
$ cwebp -lossless source.png -o output.webp
```

For lossless, control compression with -z (0-9 with 9 being highest compression but also longest encoding).
