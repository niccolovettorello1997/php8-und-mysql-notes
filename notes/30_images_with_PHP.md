# Chapter 30 – Images with PHP

## Sections
1. Preparation  
2. Using GD2  
3. ImageMagick  
4. GMagick  
5. NetPBM  

---

## Summary
This chapter covers **image processing in PHP**, focusing on different libraries and tools.  
Working with images is important for **web applications** like galleries, CMS, e-commerce, and dynamic image generation.  

---

## Key Concepts

### 1. Preparation
- PHP provides extensions and bindings to popular **image processing libraries**.  
- Typical operations:  
  - Resizing, cropping, rotating.  
  - Adding watermarks or text overlays.  
  - Generating images dynamically (charts, captchas).  
- Choice of library depends on **performance needs, format support, and hosting environment**.  

---

### 2. Using GD2
- **GD2** is bundled with PHP (commonly available).  
- Supports basic image creation and manipulation.  
- Formats: PNG, JPEG, GIF, WebP (depending on compilation).  

Example:  
```php
// Create an empty image
$image = imagecreatetruecolor(200, 100);

// Allocate colors
$bg = imagecolorallocate($image, 255, 255, 255);
$textColor = imagecolorallocate($image, 0, 0, 0);

// Fill background
imagefilledrectangle($image, 0, 0, 200, 100, $bg);

// Add text
imagestring($image, 5, 50, 40, "Hello GD2", $textColor);

// Output to browser
header("Content-Type: image/png");
imagepng($image);
imagedestroy($image);
```

---

### 3. ImageMagick

* External, powerful image manipulation toolkit.
* Supports **hundreds of formats** and advanced effects.
* PHP extension: `imagick`.
* Used for **professional-quality image transformations**.

Example:

```php
$image = new Imagick("photo.jpg");
$image->thumbnailImage(200, 0);
$image->writeImage("thumbnail.jpg");
```

---

### 4. GMagick

* Alternative PHP extension binding to **GraphicsMagick** (a fork of ImageMagick).
* Lighter and faster in some scenarios.
* API is similar to `Imagick`.

Example:

```php
$image = new Gmagick("photo.jpg");
$image->resizeimage(200, 200, Gmagick::FILTER_LANCZOS, 1);
$image->write("resized.jpg");
```

---

### 5. NetPBM

* **Portable Bitmap Utilities** (command-line tools).
* Can be used with PHP via `exec()` or process pipes.
* Less common today, but still powerful for batch processing.

---

## Notes

* **GD2**: Best for simple dynamic images, very portable.
* **Imagick / GMagick**: Best for advanced manipulation and wide format support.
* **NetPBM**: Legacy, niche use cases.
* Consider performance and hosting restrictions before choosing a library.
* For **modern projects**, Imagick is usually the preferred option.