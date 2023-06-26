# Post-Quantum-Authentication-on-the-Web
This is a top-level/index repository for implementing ESP32-embedded-device-enabled post-quantum authentication in the web application and web services.

## Introduction
This project is a proof-of-concept for an article (link added later). It provides reference implementation of post-quantum algorithms in an existing [authentication framework](https://github.com/Muzosh/Smart-Card-Authentication-On-The-Web), where instead of using smart-cards as user devices, an ESP32 embedded device is used.

## General infrastructure overview
![image](https://github.com/Muzosh/Post-Quantum-Authentication-on-the-Web/assets/30979983/bd86e6b9-29b3-4146-8d96-3fd7efcb6e1c)


## Repositories overview
![image](https://github.com/Muzosh/Post-Quantum-Authentication-on-the-Web/assets/30979983/9c421367-163f-4b8d-a021-f9a6ded5cf85)
> Note: some repository names are not equal to separate repositories, but only refer to a specific branch in base repository. This is done to enable future pull requests. Just follow the links below to go to the specific changes.

Following list is sorted by the lowest dependency (meaning that first listed project do not require any dependencies to other listed projects; bottom ones are dependent on top ones):
* [`liboqs-php`](https://github.com/Muzosh/liboqs-php) - PHP wrapper for libOQS library that enables PHP developers to work with post-quantum algorithms
* [`Muzosh/liboqs-python`](https://github.com/Muzosh/liboqs-python) - custom Python wrapper for libOQS library that enables Python developers to work with post-quantum algorithms
* [`OQS-openssl-in-PHP`](https://github.com/Muzosh/OQS-openssl-in-PHP) - notes on how to use post-quantum version of OpenSSL in PHP
* [`PQC-libserial-cpp`](https://github.com/Muzosh/libserial-cpp) - an equivalent of [libpcsc-cpp](https://github.com/web-eid/libpcsc-cpp) that enables Web-eID app to communicate with USB serial devices as well
* [`PQC-libpcsc-cpp`](https://github.com/Muzosh/libpcsc-cpp/tree/feature-adapt-serial-abstraction-layer) - adaptation of existing library to the new abstraction layer in the Web-eID app
* [`PQC-phpseclib`](https://github.com/Muzosh/phpseclib/tree/feature-post-quantum-support) - Introduces post-quantum support with Dilithium5 as functional reference
  * requires: either `liboqs-php`, `OQS-openssl-in-PHP`, or `both` (via installation on the same system)
* [`PQC-web-eid-authtoken-validation-php`](https://github.com/Muzosh/web-eid-authtoken-validation-php-fork-of-official-repo/tree/feature-post-quantum-support) - PQ extension of the official [Web-eID repository](https://github.com/web-eid) for PHP back-end servers
  * requires: `PQC-phpseclib` (via composer.json - vcs dependency)
* [`PQC-twofactor-webeid`](https://github.com/Muzosh/nextcloud_twofactor_webeid) - an installable application to Nextcloud cloud storage server enabling the usage of PQC Web-eID for authenticating users into the web interface (can serve as an implementation example).
  * requires `PQC-web-eid-authtoken-validation-php` (via composer.json - vcs dependency)
* `PQC-nextcloud-docker` - development instance of PQC-ed Nextcloud server using Docker.
  * requires: `PQC-twofactor-webeid` (via git submodule)
* [`PQC-libelectronic-id`](https://github.com/Muzosh/libelectronic-id/tree/feature-abstraction-layer-and-InfinitEIDPQ) - introduces abstraction layer to introduce USB serial devices on top of smart cards and adds interface implementation for InfinitEIDPQ embedded device
  * requires: `PQC-libserial-cpp` and `PQC-libpcsc-cpp` (via git submodules)
* [`PQC-web-eid-app`](https://github.com/Muzosh/web-eid-app/tree/feature-abstraction-layer-and-serial-devices) - introduces abstraction layer to introduce USB serial devices on top of smart cards
  * requires: `PQC-libelectronic-id` (via git submodules)
* [`InfinitEIDPQ`](https://github.com/Muzosh/InfinitEIDPQ) - contains full-fledged applet for ESP32 firmware that enables post-quantum authentication on the web using embedded devices, and administration application for device management
  * requires: `Muzosh/liboqs-python`
