[![Example Code header](https://github.com/newrelic/opensource-website/raw/master/src/images/categories/Example_Code.png)](https://opensource.newrelic.com/oss-category/#example-code)

Introduction
----------------------
[![PyPI](https://img.shields.io/badge/pypi_newrelic_telemetry_sdk-0.4.2-0ab0bf?logo=image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI2NCIgaGVpZ2h0PSI2NCI+PHBhdGggZD0iTTYzLjUzIDI1LjE0NWMtMy4wMDMtMTMuOC0xOS41NS0yMS45MTQtMzYuOTY2LTE4LjEzUy0yLjUzIDI1LjA2LjQ3IDM4Ljg1NHMxOS41NSAyMS45MTggMzYuOTYyIDE4LjEzIDI5LjA5OC0xOC4wMjcgMjYuMS0zMS44NHpNMzIuMDAyIDQ0LjcyYTEyLjcyIDEyLjcyIDAgMCAxLTguOTk0LTIxLjcxNCAxMi43MiAxMi43MiAwIDAgMSAyMS43MTQgOC45OTRjMCA3LjAyNS01LjY5NSAxMi43Mi0xMi43MiAxMi43MnoiIGZpbGw9IiMwMDhjOTkiLz48cGF0aCBkPSJNMzQuODEzIDE0LjE5MmMtMTAuMDg2LjAwMi0xOC4yNiA4LjE4LTE4LjI2IDE4LjI2NnM4LjE3OCAxOC4yNiAxOC4yNjQgMTguMjZTNTMuMDggNDIuNTQgNTMuMDggMzIuNDU1YzAtNC44NDQtMS45MjUtOS41LTUuMzUtMTIuOTE1cy04LjA3Mi01LjM1LTEyLjkxNi01LjM0OHpNMzEuOTk4IDQzLjFhMTEuMTEgMTEuMTEgMCAwIDEtNy44NTYtMTguOTY2IDExLjExIDExLjExIDAgMCAxIDE4Ljk2NiA3Ljg1NmMwIDYuMTM0LTQuOTcyIDExLjEwOC0xMS4xMDYgMTEuMXoiIGZpbGw9IiM3MGNjZDMiLz48L3N2Zz4=)](https://pypi.org/project/newrelic-telemetry-sdk/0.4.2/)  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

This project aims to demonstrates the New Relic Telemetry SDK usage for Python for retrieving Owlet Smart Sock v2/v3 Sensor statistics such as heart rate, oxygen level, etc. 

The script's implementation was made possible after others first reversed engineered the android app to understand how the data is recorded and fetched. Credit for the only known login API to work goes to @mbevand for their work in https://github.com/mbevand/owlet_monitor/blob/master/owlet_monitor. This script herein has been significantly enhanced for stability logic and Sock v3 sensor properties. 

The script batch sends metrics every 10 seconds in New Relic metric format. All credentials including `NEW_RELIC_INSERT_KEY OWLET_USER`, `OWLET_PASS`, and `OWLET_REGION` must be passed via environment variables. Log messages are printed on stdout in INFO level fasion.


Technical details
----------------------
* The owlet account email and password are validated using [Firebase Authentication](https://firebase.google.com/docs/auth) — this returns a JWT
* A GET request authenticated with the JWT is made to https://ayla-sso.owletdata.com/mini/ — this returns a `mini_token`
* The `mini_token` is used to sign into the [Ayla Networks cloud API](https://developer.aylanetworks.com/apibrowser/)
* Heart rate, oxygen level, etc are periodically fetched from the Ayla API

Many details (app id/secret, property names) have been reverse-enginered from Owlet's Android app.

You can import the "dashboard.json" directory to your new relic account to see the chart and metics.

![dashboard](https://github.com/andrew-lozoya/owletsock-newrelic/blob/main/images/Screenshot_2021-05-25%20Baby%20Board%20share%20New%20Relic%20One.png)
