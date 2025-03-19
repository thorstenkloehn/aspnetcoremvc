# ASP.NET Core MVC Konfiguration

Erstelle eine Datei `appsettings.json` im Projektverzeichnis und füge folgenden Inhalt ein:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Database=test;Username=test;Password=Test"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}

```
## Datenbankeinrichten
Erstelle eine Datenbank
```bash
cd $HOME
sudo -u postgres -i
createuser thorsten
createdb -E UTF8 -O thorsten thorsten
psql -d thorsten -c "CREATE EXTENSION postgis;" # Erweiterung hinzufügen
psql -d thorsten -c "CREATE EXTENSION hstore;" # Erweiterung hinzufügen
psql -d thorsten -c "CREATE EXTENSION vector;" # Erweiterung hinzufügen
psql -d thorsten -c "ALTER TABLE geometry_columns OWNER TO thorsten;" # Rechte setzen
psql -d thorsten -c "ALTER TABLE spatial_ref_sys OWNER TO thorsten;" # Rechte setzen
psql -d thorsten -c "\password thorsten"
exit # Ausloggen
```
## Laden der OpenStreetMap Daten für Ahrensburg
```bash
cd $HOME
wget https://download.geofabrik.de/europe/germany/schleswig-holstein-latest.osm.pbf
osmosis --read-pbf file=schleswig-holstein-latest.osm.pbf --bounding-box left=10.1141 right=10.3716 top=53.7136 bottom=53.6249 --write-pbf file=ahrensburg.pbf

osm2pgsql  -d thorsten --create  -G --hstore  ahrensburg.pbf
```
## Vorhandene Datenbank einrichten
```bash
cd $HOME/aspnetcoremvc
dotnet ef dbcontext scaffold "Host=localhost;Database=Test;Username=Test;Password=Test" Npgsql.EntityFrameworkCore.PostgreSQL -o Models -c ApplicationDbContext -t planet_osm_line -t planet_osm_point -t planet_osm_point -t planet_osm_polygon -t planet_osm_roads -
```
## Migrationen erstellen
```bash
dotnet ef migrations add InitialCreate --context ahrensburg.city.Data.ApplicationDbContext
dotnet ef database update --context ahrensburg.city.Data.ApplicationDbContext
```