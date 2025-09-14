# Chapter 29 – XML

## Sections
1. Preparation  
2. Accessing XML with PHP  
3. XMLReader and XMLWriter  
4. EXIF  

---

## Summary
This chapter introduces **working with XML in PHP**, covering built-in functions, parsing methods, and metadata extraction (EXIF).  
XML is often used for **configuration, data exchange, and interoperability**.  

---

## Key Concepts

### 1. Preparation
- **XML (eXtensible Markup Language)** is a markup language for structured data.  
- Common use cases:  
  - Data exchange between systems.  
  - Configuration files.  
  - Legacy systems integration.  
- PHP offers **multiple APIs** to parse, read, and generate XML.  

---

### 2. Accessing XML with PHP
- Main approaches:  
  - **SimpleXML**: Easy-to-use, object-oriented interface for XML.  
  - **DOMDocument**: Full XML DOM manipulation, more powerful but verbose.  

Example with **SimpleXML**:  
```php
$xml = simplexml_load_file("books.xml");
foreach ($xml->book as $book) {
    echo $book->title . PHP_EOL;
}
```

Example with **DOMDocument**:

```php
$dom = new DOMDocument();
$dom->load("books.xml");
$titles = $dom->getElementsByTagName("title");
foreach ($titles as $title) {
    echo $title->nodeValue . PHP_EOL;
}
```

---

### 3. XMLReader and XMLWriter

* **XMLReader**: Forward-only, streaming parser (efficient for large XML).

  * Reads XML sequentially without loading the whole file in memory.
  * Useful for **big data files**.

Example:

```php
$reader = new XMLReader();
$reader->open("books.xml");
while ($reader->read()) {
    if ($reader->nodeType == XMLReader::ELEMENT && $reader->name == "title") {
        echo $reader->readInnerXml() . PHP_EOL;
    }
}
$reader->close();
```

* **XMLWriter**: Used to create XML files programmatically.

Example:

```php
$writer = new XMLWriter();
$writer->openURI("output.xml");
$writer->startDocument("1.0", "UTF-8");
$writer->startElement("books");
$writer->writeElement("title", "Learning PHP");
$writer->endElement(); // books
$writer->endDocument();
$writer->flush();
```

---

### 4. EXIF

* **EXIF (Exchangeable Image File Format)** stores metadata in image files (JPEG, TIFF).
* Common metadata: **camera model, GPS coordinates, timestamp**.
* PHP can read EXIF data using `exif_read_data()`.

Example:

```php
$exif = exif_read_data("photo.jpg");
echo "Camera: " . $exif['Model'] . PHP_EOL;
echo "Date: " . $exif['DateTime'] . PHP_EOL;
```

---

## Notes

* **SimpleXML** is best for quick scripts.
* **DOMDocument** is better for complex manipulation.
* **XMLReader/XMLWriter** scale to large datasets.
* **EXIF** is useful for apps dealing with images (galleries, geo-tagging).
* XML is less popular today compared to **JSON**, but still relevant in enterprise and legacy contexts.