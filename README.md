# Magento compressed sample data

The official Magento CE 1.9 sample data archives are far too big (~420 MB)!

As [Vinai Kopp's compressed sample data repository](https://github.com/Vinai/compressed-magento-sample-data/) is not up-to-date at the time of writing, I decided to create my own version.

Sample data for Magento CE 1.6 - 1.8 is not especially big, I just wanted to have it here too.

## What has been done?

* Remove useless files

```sh
rm -rf media/catalog/product/cache/* media/tmp/*
```

* Compress JPG files with [jpegoptim](http://www.kokkonen.net/tjko/projects.html)

```sh
find . -type f -name "*.jpg" -exec jpegoptim -m40 --strip-all {} \;
```

* Optimize PNG files with [pngquant](https://pngquant.org/)

```sh
find . -type f -name "*.png" -exec pngquant --ext .png --force --skip-if-larger {} \;
```

* Re-encode MP3 files with a 32 kbps bitrate with [lame](http://lame.sourceforge.net/)

```sh
find . -type f -name '*.mp3' -exec sh -c 'lame -b 32 "$0" "$0"-32 && mv "$0"-32 "$0"' {} \;
```

For 1.6 sample data, only the JPG files are to process.

## For what results?

Here are the sizes of the sample data folder, uncompressed:

* 1\.6\.1\.0 : 14 MB => 6 MB
* 1\.9\.0\.0 : 468 MB => 80 MB
* 1\.9\.1\.0 : 473 MB => 80 MB
* 1\.9\.2\.4 : 473 MB => 80 MB

Once compressed, 1.9 archives are about: zip 64 MB ; tar\.gz 62 MB ; tar\.bz2 55 MB
