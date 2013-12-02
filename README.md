Data-Download
=============

#MODIS Snow Cover Data

import sys
sys.path.insert(0,'files/python')
import gdal
import numpy as np
import numpy.ma as ma
from raster_mask import raster_mask
import glob
import os
from osgeo import ogr,osr
import pylab as plt

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

[[[FLAG- print parts not needed in final code]]]]
    
data = {}
    
def snow_cover(modis_file, \
                          qa_layer = 'Snow_Spatial_QA', \
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
    
    
    #vector mask
    
    from raster_mask import raster_mask
    fname = 'HDF4_EOS:EOS_GRID:"%s":%s'%(modis_file,data_layer)
    mask = raster_mask2(fname,\
                target_vector_file="files/data/Hydrologic_Units/HUC_Polygons.shp",\
                attribute_filter=2)
    plt.imshow(mask)
    plt.colorbar()

rowpix,colpix = np.where(mask == False)
mincol,maxcol = min(colpix),max(colpix)
minrow,maxrow = min(rowpix),max(rowpix)
ncol = maxcol - mincol + 1
nrow = maxrow - minrow + 1
small_mask = mask[minrow:minrow+nrow,mincol:mincol+ncol]





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

for line_data in required_data: #loop over each line
    day_data = line_data.split() #strings split on the white space
    data.append(day_data)
print data[0][0]
temp_data = []
for line in data:
    temp_data.append(line[0:-3])
#years are defined
years = '2009' and '2010'
for line in temp_data:
    np.where(years)
    

    
newtemp_data = []
for line in temp_data:
    if (line.startswith("2009")) and (line.startswith("2010"):
        newtemp_data.append(temp_data)
        

        
        
    
[[[[[[#FLAG - #convert data to float
    for column,this_element in enumerate(day_data):
        day_data[column] = float(this_element)  ]]]]]]


#Boundary Data

import sys
sys.path.insert(0,'files/python')
from raster_mask import *
m = raster_mask2(fname,\target_vector_file="files/data/Hydrologic_Units/HUC_Polygons.shp",\attribute_filter=2)

#individual steps

New MODIS SNow Cover Code
modis_files = 'files/data/MODIS_Snow_Data
MOD10A1.A2009001.h09v05.005.2009009120443.hdf'
target_vector_file = file
g = gdal.Open(modis_file)
subdatasets = g.GetSubDatasets()
for fname, name in subdatasets:
    print name
    print "\t", fname
data = {}
data_layers = ["Fractional_Snow_Cover","Snow_Spatial_QA"]
file_template = 'HDF4_EOS:EOS_GRID:"%s":MOD_Grid_Snow_500m:%s'
for i,layer in enumerate(data_layers):
        this_file = file_template % (modis_file, layer)
        g = gdal.Open(this_file)
        data[layer] = g.ReadAsArray()
snow = data['Fractional_Snow_Cover']
plt.imshow(snow)
plt.colorbar()
qa = data['Snow_Spatial_QA']
qa = qa & 1
qa_mask = np.ma.array ( snow, mask=qa )


years = '2009' and '2010'
sensors = 'MOD10A1' and 'MYD10A1'
modis_files = np.sort(glob.glob('files/data/MODIS_Snow_Data/%s.A%d*.h09v05.*.hdf'%(sensors,years))

def snow_cover(modis_files):
    g = gdal.Open(modis_file)
    subdatasets = g.GetSubDatasets()
    data_layers = [ "Fractional_Snow_Cover", "Snow_Spatial_QA" ]
    data = {}
    file_template = 'HDF4_EOS:EOS_GRID:"%s":MOD_Grid_Snow_500m:%s'
    for i,layer in enumerate(data_layers):
        this_file = file_template % (modis_file, layer)
        g = gdal.Open(this_file)
        data[layer] = g.ReadAsArray()
    snow = data['Fractional_Snow_Cover']
    qa = data['Snow_Spatial_QA']
    qa = qa & 1
    qa_mask = np.ma.array ( snow, mask=qa )
    return qa_mask
    
#loop for all images
modis_snow = []
for f in modis_files:
    modis_snow.append(snow_cover(f))
snow_cover = np.ma.array(snow_cover)








