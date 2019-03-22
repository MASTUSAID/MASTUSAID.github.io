# Geoserver Configuration

GeoServer is used by MAST DMI for displaying various map layers. You can publish and link to DMI any type of layers, but there are a few important ones, which must be configured in GeoServer in order for DMI to function properly. They include land parcels layer, resources layers and area of interest layer.

Before starting GeoServer configuration, open your browser and type in IP address of your Tomcat server with '/geoserver/ at the end: `http://localhost:8080/geoserver/`

In this example we are using localhost, but you should replace it with your IP address
.
By default GeoServer has the username `admin` with password `geoserver`. Use these for accessing GeoServer for the first time, but it’s highly recommended that you change this password to something more secure.

## Create Namespace
First, we have to create the mast namespace, where all further data stores, layers and styles will be configured. Follow the steps below:
1.	Login into GeoServer.
2.	Click **Workspaces** in the left menu.
3.	Click **Add new workspace** link.
4.	Enter the following values: 
   * Name = Mast
   * Namespace = `http://localhost:8080/` (change localhost to IP address of Tomcat server if you want to access DMI from the network)
   * Tick **Default Workspace**
5.	Click **Submit** button

## Enable anonymous access
In newer GeoServer versions, anonymous “write” access is turned off and therefore you won’t be able to do spatial editing from the MAST DMI. Make sure that anonymous “write” access is enabled by following the steps below:
1.	Click on the Data option under Security main menu.
2.	In the list of rules, check if `ROLE_ANONYMOUS` is present for `*.*.w` rule.
3.	If anonymous role is missing, click on the `*.*.w` rule.
4.	On the next screen select `ROLE_ANONYMOUS` in the available roles and click add button “=>” to add it into Selected Roles.
5.	Click Save button.

## Publish Parcels Layer
For displaying land parcels on the map control in DMI, they have to be published on GeoServer first. If you initialized the MAST database from the script in this GitHub account, it already has settings to read the core Geoserver layers from localhost. If you are testing your server from a different computer, these layers’ IP address has to be changed in the database. See the `Adjust layers URL` section for more details.
Start publishing the parcels layers by creating new a data store:
1.	Click **Stores** in the main menu.
2.	Click **Add new store**.
3.	Click on **PostGIS vector data source**.
4.	Enter the following parameters:
   -	Workspace = Mast
   -	Data Source Name = MastDB
   -	Host = localhost (or IP address if your database on the different server)
   -	Port: 5432
   -	Database = mast
   -	User = postgres
   -	Password = [your_postgres_password]
   -	Expose primary keys = yes (ticked)
5.	Click **Save** button
If all parameters are provided correctly, you will see the next screen with the list of tables, available in the database. If you have any issues, see the Known Issues section for more details regarding PostgreSQL drivers in GeoServer.

Go through the listed tables and find `la_spatialunit_land`. Click the **Publish** link against this table. Alternatively you can go through Layers menu and select Add a new layer option. Make sure the following parameters are set for the land parcels layer:
1.	Name = la_spatialunit_land
2.	Title = Land Parcels
3.	Native SRS = EPSG:4326
4.	Declared SRS = EPSG:4326
5.	Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
6.	Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
7.	Click **Save** button
After  saving, the layer will appear in the list of layers (under the **Layers** menu)

## Publish Area of Interest Layer
The Area of Interest area layer is used for displaying designated areas, which can be further assigned to specific para-surveyor for limiting his area of field surveys. Since we have already created MAST database source, we simply need to publish a new layer. Follow these steps below:
1.	Click **Layers** menu.
2.	Click **Add a new layer** link.
3.	Select **Mast:MastDB** data source.
4.	Look for `la_spatialunit_aoi` table and click the **Publish**.
5.	Provide the following values:
   - Name = la_spatialunit_aoi
   - Title = AOI
   - Native SRS = EPSG:4326
   - Declared SRS = EPSG:4326
   - Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
   - Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
6.	Click **Save** button

## Publish resource (land) layer
MAST allows the capture of various resource types in the field. They can be in the form of a polygon, line or point. Follow these steps below to publish polygon resources:
1.	Click **Layers** menu.
2.	Click **Add a new layer** link.
3.	Select **Mast:MastDB** data source.
4.	Look for `la_spatialunit_resource_land` table and click **Publish**.
5.	Provide the following values:
   - Name = la_spatialunit_resource_land
   - Title = Resource Land
   - Native SRS = EPSG:4326
   - Declared SRS = EPSG:4326
   - Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
   - Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
6.	Click **Save** button

## Publish resource (line) layer
To publish line resources, follow these steps below:
1.	Click **Layers** menu.
2.	Click **Add a new layer** link.
3.	Select **Mast:MastDB** data source.
4.	Look for `la_spatialunit_resource_line` table and click **Publish**.
5.	Provide the following values:
   - Name = la_spatialunit_resource_line
   - Title = Resource Lines
   - Native SRS = EPSG:4326
   - Declared SRS = EPSG:4326
   - Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
   - Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
6.	Click **Save** button

## Publish resource (point) layer
For publishing point resources, follow these steps below:
1.	Click **Layers** menu.
2.	Click **Add a new layer** link.
3.	Select **Mast:MastDB** data source.
4.	Look for `la_spatialunit_resource_point` table and click **Publish**.
5.	Provide the following values:
   - Name = la_spatialunit_resource_point
   - Title = Resource Points
   - Native SRS = EPSG:4326
   - Declared SRS = EPSG:4326
   - Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
   - Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
6.	Click **Save** button

Vertices layer is used for showing land parcel vertices, when producing various print outs (e.g. land certificate). Follow these steps below:
Click **Layers** menu.
2.	Click **Add a new layer** link.
3.	Select **Mast:MastDB** data source.
4.	Look for `vertexlabel` table and click **Publish**.
5.	Provide the following values:
   - Name = vertexlabel
   - Title = vertexlabel
   - Native SRS = EPSG:4326
   - Declared SRS = EPSG:4326
   - Click **Compute from SRS bounds** to calculate bounding box. You can use **Compute from data** if you have already some data.
   - Click **Compute from native bounds** to set **Lat/Lon Bounding Box**
6.	Switch to **Publishing** tab and select **point style** in the **Default Style** dropdown box.
7.	Click Save button

## Adjust Layers URL
The default MAST database comes with predefined list of layers, configured for http://localhost:8080 address. If you have a different port number or are planning to test MAST from the network using real IP address of the server, you need to update the layers in the `la_spatialsource_layer` table. Simply run the following query on your MAST database:
```
update la_spatialsource_layer set location = 'http://your_ip_address:port_number/geoserver/wfs?';
```
Change “your_ip_address” and “port_number” to appropriate values, according to your configuration. In Ubuntu, using the psql client:
```
$ sudo -u postgres psql
postgres=# \c mast
mast=# update la_spatialsource_layer set location = 'http://your_ip_address:port_number/geoserver/wfs?';
```

## Known Issues
### Java
When installing Tomcat on Windows system using Java 8, there may be an issue with starting the MAST DMI application. In the log files of Tomcat you will find the following error:
```
Property 'passwordEncoder' threw exception; nested exception is org.jasypt.exceptions.EncryptionOperationNotPossibleException
```
In order to resolve this, download Java 7 Cryptography Extensions from the following link:
http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html 
Extract and copy over downloaded files into your JRE installation folder under `lib/security`. They have to be placed in the jre folder according to your JAVA_HOME configuration.

## GeoServer JDBC driver for PostgreSQL
GeoServer comes with a PostgreSQL JDBC driver, but sometimes it may not match your database version. Since we are deploying JDBC driver into Tomcat libraries, you can try and delete this driver from the GeoServer folder. Geoserver folder is created under Tomcat `webapps` folder after you start your Tomcat for the first time. Go to the GeoServer’s lib folder (e.g. `/opt/tomcat/webapps/geoserver/WEB-INF/lib`) and delete the postgresql file (e.g. `postgresql-42.1.1.jar`).
After deleting the file, you will need to restart your Tomcat. Make sure to give it some time (30 seconds or so) before starting Tomcat again.
```
$ sudo /opt/tomcat/bin/shutdown.sh
$ sudo /opt/tomcat/bin/startup.sh
```

