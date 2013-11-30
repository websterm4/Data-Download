Data-Download
=============

#MODIS Snow Cover Data

import gdal
import numpy as np
import numpy.ma as ma

#for one file:
modis_file = 'MOD10A1.A2009001.h09v05.005.2009009120443.hdf'
target_vector_file = file
g = gdal.Open(modis_file)

subdatasets = g.GetSubDatasets()
for fname, name in subdatasets:
    print name
    print "\t", fname
    
data_layers = [ "Fractional_Snow_Cover" , "Snow_Spatial_QA" ]
file_template = 'HDF4_EOS:EOS_GRID:"%s":MOD_Grid_Snow_500m:%s'
    
data ={}
for i,layer in enumerate(data_layers):
    this_file = file_template % (modis_file, layer)
    g = gdal.Open(this_file)
    data[layer] = g.ReadAsArray()
    
snow_cover = data['Fractional_Snow_Cover']
qa = data['Snow_Spatial_QA']

np.unique(qa)
qa = qa & 1
cloud_mask = np.ma.array ( snow_cover, mask=qa )
#masked data showing only 'good quality' data, clouds represent the bad quality data

#Discharge Data
#Reading the data invloved using the 'Save as' function in the browser

import numpy as np

file = 'files/data/delnorte.dat'
data = np.loadtxt(file,usecols=(2,3),unpack=True,dtype=str)
plt.plot(data[1].astype(float))
import datetime
ds = np.array(data[0][0].split('-')).astype(int)
year,doy = datetime.datetime(ds[0],ds[1],ds[2]).strftime('%Y %j').split()
#All of the above code taken directly from the course notes


#Temperature Data
#Reading the data invloved using the 'Save as' function in the browser


#Boundary Data

import sys
sys.path.insert(0,'files/python')
from raster_mask import *
m = raster_mask2(fname,\target_vector_file="files/data/Hydrologic_Units/HUC_Polygons.shp",\attribute_filter=2)


