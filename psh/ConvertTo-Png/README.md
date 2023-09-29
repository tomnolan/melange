# ConvertTo-Png

> A PowerShell script that converts image files to PNG format

This is a direct conversion from David Anson's [ConvertTo-Jpeg](https://github.com/DavidAnson/ConvertTo-Jpeg)

## Overview

`ConvertTo-Png.ps1` is a [PowerShell](https://en.wikipedia.org/wiki/PowerShell) script that uses the [Windows.Graphics.Imaging API](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.imaging) to create a PNG-encoded copy of each image that is passed to it.
(The original file is not modified.)

## Related

- [ConvertTo-Jpeg.ps1](https://github.com/DavidAnson/ConvertTo-Jpeg): A PowerShell script that converts RAW (and other) image files to the widely-supported JPEG format
- [ConvertTo-Heic.ps1](https://github.com/DavidAnson/ConvertTo-Heic): A PowerShell script that converts image files to the efficient HEIC format

## Examples

### Converting Files

Passing parameters:

```PowerShell
PS C:\T> .\ConvertTo-Png.ps1 C:\T\Pictures\IMG_1234.HEIC C:\T\Pictures\IMG_5678.HEIC C:\T\Pictures\IMG_90.PNG
C:\T\Pictures\IMG_1234.HEIC -> IMG_1234.HEIC.png
C:\T\Pictures\IMG_5678.HEIC -> IMG_5678.HEIC.png
C:\T\Pictures\IMG_90.PNG [Already PNG]
```

Pipeline via `dir`:

```PowerShell
PS C:\T> dir C:\T\Pictures | .\ConvertTo-Png.ps1
C:\T\Pictures\IMG_1234.HEIC -> IMG_1234.HEIC.png
C:\T\Pictures\IMG_5678.HEIC -> IMG_5678.HEIC.png
C:\T\Pictures\Kitten.png [Already PNG]
C:\T\Pictures\Notes.txt [Unsupported]
```

Pipeline via `Get-ChildItem`:

```PowerShell
PS C:\T> Get-ChildItem C:\T\Pictures -Filter *.HEIC | .\ConvertTo-Png.ps1
C:\T\Pictures\IMG_1234.HEIC -> IMG_1234.HEIC.png
C:\T\Pictures\IMG_5678.HEIC -> IMG_5678.HEIC.png
```

## Formats

| Decoder                      | Extensions |
| ---------------------------- | ---------- |
| BMP Decoder                  | .BMP .DIB .RLE |
| CUR Decoder                  | .CUR |
| DDS Decoder                  | .DDS |
| DNG Decoder                  | .DNG |
| GIF Decoder                  | .GIF |
| ICO Decoder                  | .ICO .ICON |
| JPEG Decoder                 | .EXIF .JFIF .JPE .JPEG .JPG |
| Microsoft Camera Raw Decoder | .ARW .CR2 .CRW .DNG .ERF .KDC .MRW .NEF .NRW .ORF .PEF .RAF .RAW .RW2 .RWL .SR2 .SRW |
| *Microsoft HEIF Decoder*     | .AVCI .AVCS .HEIC .HEICS .HEIF .HEIFS |
| *Microsoft Webp Decoder*     | .WEBP |
| PNG Decoder                  | .PNG |
| TIFF Decoder                 | .TIF .TIFF |
| WMPhoto Decoder              | .JXR .WDP |

## HEIC/HEIF

Windows 10's April 2018 Update (version 1803) added support for [HEIC/HEIF images](https://en.wikipedia.org/wiki/High_Efficiency_Image_File_Format) to the Windows.Graphics.Imaging API.
`ConvertTo-Jpeg.ps1` uses the new decoder automatically if it's available.
To enable the decoder, install the Microsoft [HEIF and HEVC Media Extensions](https://www.microsoft.com/store/productId/9NTLD6MSD8BM) bundle (or else both of [HEVC Video Extensions](https://www.microsoft.com/store/productId/9NMZLZ57R3T7) and [HEIF Image Extensions](https://www.microsoft.com/store/productId/9PMMSR1CGPWG)).
Once done, the built-in Photos app (and other programs that use the Windows.Graphics.Imaging API) will be able to open HEIC/HEIF images.

## WEBP

If the default support for [WebP](https://en.wikipedia.org/wiki/WebP) images is missing or incomplete, consider installing the Microsoft [Webp Image Extensions](https://www.microsoft.com/en-us/p/webp-image-extensions/9pg2dk419drg).
As above, the built-in Photos app is a great way to verify support for WEBP images.
