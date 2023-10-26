+++
author = "Frank Adrian"
comments = true
cover = "/uploads/blank-power-query.png"
date = "2023-10-26T23:00:00+02:00"
tags = ["influxdb", "excel", "power query"]
title = "How to import influxdb data to Excel sheet with power query"
draft = false
+++

Recently a client needed some data from his influxdb linked to an Excel sheet. 
This can be achieved with a Power Query, from your Excel Workbook choose **Data -> Get Data (Power Query) -> Blank query**

![blank-power-query.png](/uploads/blank-power-query.png)

Replace the existing code with the following code:
```
let
    url = "https://localhost:8086",
    orgName= "MyOrg",
    token = "MyOrganisation",
    query = Text.ToBinary("

from(bucket: ""climate"")
  |> range(start: -7d)
  |> filter(fn: (r) => r[""_measurement""] == ""climate"")
  |> filter(fn: (r) => r[""_field""] == ""humidity"" or r[""_field""] == ""temperature"")
  |> filter(fn: (r) => r[""deviceName""] =~ /U1/)
  |> pivot(rowKey: [""_time""], columnKey: [""_field""], valueColumn: ""_value"")
  |> keep(columns: [""_time"", ""deviceName"", ""humidity"", ""temperature""])

"),
    options = [
        Headers = [
            Authorization="Token " & token,
            accept="application/csv",
            #"content-type"="application/vnd.flux"],
        RelativePath="api/v2/query",
        Query=[org=orgName],
        Content=query
    ],
    result = Table.PromoteHeaders(Csv.Document(Web.Contents(url, options)))
in
    result
```


### Notes:

- set `url`, `orgName`, `token` and `query` 
- Flux query goes in the `query` parameter; Note the escaped double quotes ("")
- replace **https://localhost:8086** with your influxdb host
- replace **myToken** with an Access Token with Read access to the required Bucket(s)
- replace **MyOrganisation** with your organisation name
- tested with Excel for Mac Version 16.78


