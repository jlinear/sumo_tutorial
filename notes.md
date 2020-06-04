# Notes on SUMO tutorial

## Manual creation of Road Network

1. Node file - .nod.xml
2. Edge file - .edg.xml
3. Edge type file - .type.xml
4. Network creation from above files
5. Route file - .rou.xml

Then, node file + edge file + type file ==> net file
``` bash
netconvert --node-files my_nodes.nod.xml --edge-files my_edge.edg.xml -t my_type.type.xml -o my_net.net.xml
```

Then define route files and sumo configuration files
Run the simulation via SUMO GUI

## From OSM to network + Random trips

1. download map from OSM
2. convert map into SUMO road network
3. add random trips and routes

**Get osm map** (from osm boundingbox to .osm.xml):
```bash
python /usr/share/sumo/tools/osmGet.py -b "W, S, E, N" -d $output_directory$ -p $prefix$
```

**Build map** (from osm.xml to .net.xml + .netcfg):
```bash
python /usr/share/sumo/tools/osmBuild.py -f $PATH_TO_RAW_OSM$ -d $OUTPUT_DIRECTORY$ -p $prefix$
```

Note that the build step can also be done by netconvert, but it will only give you the .net.xml file, which does not allow further edits on the network. The command is 
```bash
netconvert --osm-files map.osm -o sumo_net.net.xml
```

**Random routes**
copy and paste the "randomTrips.py" from SUMO tools folder to the working directory. Or simply call from the origin path.
```bash
python randomTrips.py -n $PATH_TO_.net.xml$ -r $OUT_PATH_TO_.rou.xml$ -e 1000 -l
```
This will give two route files, one with 'alt' in between the suffix

**Config**
Simply set up the input and time in the .sumocfg file
