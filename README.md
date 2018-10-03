# Create-Points
Create points at alternate side of a line 

# Import arcpy module
import arcpy

# Script arguments
New_Shapefile_shp = arcpy.GetParameterAsText(0)
if New_Shapefile_shp == '#' or not New_Shapefile_shp:
    New_Shapefile_shp = "E:\\Solution\\New_Shapefile.shp" # provide a default value if unspecified

output_event_table1 = arcpy.GetParameterAsText(1)
if output_event_table1 == '#' or not output_event_table1:
    output_event_table1 = "E:\\Solution\\output_event_table1" # provide a default value if unspecified

# Local variables:
New_Shapefile_create_routes_shp = New_Shapefile_shp
output_points = New_Shapefile_create_routes_shp

# Process: Create Routes
arcpy.CreateRoutes_lr(New_Shapefile_shp, "Length", New_Shapefile_create_routes_shp, "LENGTH", "", "", "UPPER_LEFT", "1", "0", "IGNORE", "INDEX")

# Process: Make Route Event Layer
arcpy.MakeRouteEventLayer_lr(New_Shapefile_create_routes_shp, "Length", output_event_table1, "ROUTE_ID POINT MEASURE", output_points, "", "NO_ERROR_FIELD", "NO_ANGLE_FIELD", "NORMAL", "ANGLE", "LEFT", "POINT")
