---
author: "Michael Lane"
date: 2020-05-14
linktitle: Open API
title: Open API
highlight: true
weight: 20
keywords:
- api
- swagger
- open api
- OAS
- reef-pi
- reef tank
- controller
- raspberry pi
---

## API V3

reef-pi provides http json API. Entire UI is powered by the API. API requests needs to be authenticated
using session (cookie). He is an example of gettong the list of equipment
```
curl -X POST -c cookie.txt -d '{"user":"reef-pi", "password":"reef-pi"}' http://reef-pi.local/auth/signin
curl -b cookie.txt http://reef-pi.local/api/equipment
```

<redoc spec-url='https://raw.githubusercontent.com/reef-pi/reef-pi/master/swagger.json'></redoc>
<script src="https://cdn.jsdelivr.net/npm/redoc@next/bundles/redoc.standalone.js"> </script>
