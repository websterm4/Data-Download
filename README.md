Data-Download
=============

#MODIS Snow Cover Data

import sys
import gdal
import numpy as np
import numpy.ma as ma
from osgeo import ogr,osr

#for one file, (needs changing using a common name for all files)
modis_file = 'MOD10A1.A2009001.h09v05.005.2009009120443.hdf'
target_vector_file = file
g = gdal.Open(modis_file)
#using gdal to open the image file and the datasets that it contains

#pull subdatasets from each image hdf file
subdatasets = g.GetSubDatasets()
for fname, name in subdatasets:
    print name
    print "\t", fname
    
data = {}
    
def snow_cover(modis_file, \
           qa_layer = 'Snow_Spatial_QA',\
           data_layer = ["Fractional_Snow_Cover"]):
    data_layer.append(qa_layer)
    file_template = 'HDF4_EOS:EOS_GRID:"%s":MOD_Grid_Snow_500m:%s'
    for i,layer in enumerate(data_layer):
        this_file = file_template % (modis_file, layer)
        g = gdal.Open(this_file)
        data[layer] = g.ReadAsArray()
    qa = data[qa_layer] #Quality Assurance data is pulled
    #find bit 0
    qa = qa & 1 
    odata = {}
    for layer in data_layer: #syntax here may be a problem
        odata[layer] = ma.array (data[layer],mask=qa)
    return odata
    fname = 'HDF4_EOS:EOS_GRID:"%s":%s'%(modis_file,data_layer)
    #vector mask
    sys.path.insert(0,'files/python')
    from raster_mask import *
    m = raster_mask2(fname,\
                target_vector_file="files/data/Hydrologic_Units/HUC_Polygons.shp",\
                attribute_filter=2)
    
    
plt.imshow(m)
plt.colorbar()



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

file = 'files/data/delNorteT.dat'
fp = open(file, 'r')
tdata = fp.readlines()
fp.close()
required_data = tdata[2:]
#read the data in and chop off first two lines - header and white space

data = []
#set up list to store data
line_data = '2000  1  1   44    8    0    0    0\n'
day_data = line_data.split()
for line_data in required_data: #loop over each line
    day_data = line_data.split() #strings split on the white space
    #convert data to float
    for column,this_element in enumerate(day_data):
        day_data[column] = float(this_element)
    data.append(day_data)

#Boundary Data

import sys
sys.path.insert(0,'files/python')
from raster_mask import *
m = raster_mask2(fname,\target_vector_file="files/data/Hydrologic_Units/HUC_Polygons.shp",\attribute_filter=2)



#Full code


