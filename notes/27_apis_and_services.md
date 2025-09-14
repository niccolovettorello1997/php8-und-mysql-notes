# Chapter 27 – APIs and Services

## Sections
1. Preparation  
2. REST  
3. nuSOAP  
4. PHP-SOAP  
5. UDDI  

---

## Summary
This chapter covers how PHP interacts with **external services and APIs**, focusing on REST and SOAP.  
It introduces tools and libraries for implementing and consuming APIs, along with legacy technologies like UDDI.  

---

## Key Concepts

### 1. Preparation
- APIs allow communication between systems.  
- Two main paradigms:  
  - **REST (Representational State Transfer)** → modern, HTTP-based, JSON/XML payloads.  
  - **SOAP (Simple Object Access Protocol)** → XML-based, standardized, more verbose.  
- PHP provides built-in extensions and libraries to handle both.  

---

### 2. REST
- REST uses **HTTP methods**:  
  - `GET` → retrieve data  
  - `POST` → create data  
  - `PUT/PATCH` → update data  
  - `DELETE` → delete data  
- Data format: usually **JSON**, sometimes XML.  
- Example REST request in PHP (with cURL):  

```php
$ch = curl_init("https://api.example.com/users");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);

$data = json_decode($response, true);
print_r($data);
```

* Popular PHP libraries: **Guzzle**, **Symfony HttpClient**.

---

### 3. nuSOAP

* A PHP library (third-party, not bundled) for SOAP web services.
* Enables both creating SOAP servers and clients.
* Example client:

```php
require_once("lib/nusoap.php");

$client = new nusoap_client("http://example.com/service.wsdl", true);
$result = $client->call("getUser", ["id" => 1]);
print_r($result);
```

* **Note**: nuSOAP is old and rarely used today.

---

### 4. PHP-SOAP

* Native PHP extension (`soap`) for SOAP services.
* Supports **WSDL** (Web Services Description Language).

Example SOAP client:

```php
$client = new SoapClient("http://example.com/service.wsdl");
$result = $client->getUser(1);
print_r($result);
```

* More efficient and robust than nuSOAP.
* Still relevant in enterprise contexts (banks, government, legacy systems).

---

### 5. UDDI (Universal Description, Discovery and Integration)

* Standard for discovering SOAP services.
* Works like a **registry** where services can be published and located.
* Mostly obsolete today, but historically important.

---

## Notes

* **REST** is dominant in modern PHP applications.
* **SOAP** is still required for some enterprise integrations.
* UDDI is mainly legacy knowledge.
* For practical projects, focus on **REST** and modern PHP HTTP clients.