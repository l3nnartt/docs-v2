---
title: Script Editor
description: >
  
menu:
  influxdb_cloud:
    name: Script editor
weight: 1
---

The Script Editor includes an integrated schema browser, automated script creation, script management, and helps you learn Flux faster.

- Generate a new Flux script


### Generate a new Flux script
In the Script Editor, go to Schema Browser in the upper left, and do the following:
1. Turn on the Flux Sync option. This option automatically builds a Flux script as you select the data to write or query.
2. Select data for your query: bucket, measurement, fields, and tag keys. The new design highlights the hierarchical schema of the data, and more clearly distinguishes between fields and tag keys. 
As you select data, you’ll see the Flux script auto-generated to the right. Update the Flux script by adding new functions after the auto-generated code. Note, you can also manually update the auto-generated Flux code; if you do, the Flux Sync option is turned off. 
3. Do the following:
  - To view table or graph results, click Run.
  - To save the script, click **Save**, enter a script name, description, and then click **Save** again. A message confirms the script was saved.

### Update a Flux script
Use the Flux library in the Script Editor to add new functions to update your Flux script. You can also manually type in Flux to update the auto-generated script.

To update with functions from the Flux library, do the following:
1. Hover over a function in the Flux library to see a description of what the function does, and view arguments available for the function, including which are required or optional.
2. Click a function in the Flux library to add it to your script.
3. Click **Save** to save the updated script.

### Open a Flux script
In the new Script Editor, click Open. A list of existing scripts appears, select a script, and then click Open again.

### View script results (as a table or graph)
Once you’ve generated, updated, or opened a Flux script, update the time range to run the script from the drop-down list, and then click Run. By default, results are displayed in a table. 
Do the following as needed:
To search results, enter a value to search for in the Search results field. Results are automatically filtered as you type.
To page through results, click numbers or arrows below the table.
To update the time, from the drop-down list, select UTC or Local.
To view a graph, click Graph.
To download to a CSV file, click CSV.
