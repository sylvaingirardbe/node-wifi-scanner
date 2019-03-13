#node-wifi-scanner

[![Build Status](https://travis-ci.org/sylvaingirardbe/node-wifi-scanner.svg?branch=master)](https://travis-ci.org/sylvaingirardbe/node-wifi-scanner)
[![npm](https://img.shields.io/npm/v/@curaelabs/node-wifi-scanner.svg)](https://www.npmjs.com/package/@curaelabs/node-wifi-scanner)
[![npm](https://img.shields.io/npm/dt/@curaelabs/node-wifi-scanner.svg)](https://www.npmjs.com/package/@curaelabs/node-wifi-scanner)

This package is based on Christian Kuster's `node-wifi-scanner` but with updated dependencies to remove vulnerabilities and it has his latest version published to `npm` which adds better support for Raspbian.

This module for node.js scans available wifi networks. The main purpose was to enhance my node.js based
[ZigBee Site Survey Tool](http://ancasicolica.github.io/ZigBeeSiteSurvey/) with WiFi coexistence charts. This tool
claims to be compatible with current versions of Mac OS-X, Windows and Linux so I'll fix bugs as fast as possible.
Feature extensions on the other hand are not planned.

The module was inspired from Maurice Sways "[node-wifiscanner](https://github.com/mauricesvay/node-wifiscanner)". I didn't use node-wifiscanner because I
had to handle much more complex network environments and also wanted to be independent of the operating
system language. The adaptions needed would have been too comprehensive for a pull request so I decided to write an own module.

## Operating Systems

It was tested with the following operating systems:
* Mac OS-X
* Raspbian "Stretch"

## Installation

    npm i @curaelabs/node-wifi-scanner

## Usage

    const scanner = require('@curaelabs/node-wifi-scanner');

    scanner.scan((err, networks) => {
      if (err) {
        console.error(err);
        return;
      }
      console.log(networks);
    });

The tool returns an array with objects, each object representing a network with the following properties:

* channel: WiFi channel
* ssid: SSID of the network (if available)
* mac: MAC Address of the network access point
* rssi: signal strength

In contrary to other wifi scanners no information about security is returned. This is due to the very different implementation
of the command line tools which do not allow a flawless detection.

## Technical background

The module uses command line tools for gathering the network information:

* airport on Mac OS-X: `airport -s`
* netsh on Windows: `netsh wlan show networks mode=Bssid`
* iwlist on Linux: `iwlist scan`


Unfortunately, Mac OS-X and Windows use the system language for the output which requires a quite
generic way of parsing the data. If you experience any troubles, please create a GitHub issue and supply
the output of the tool.

## License

The MIT License (MIT)

Copyright (c) 2019 Sylvain Girard

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

