Data-Download
=============

#MODIS Snow Cover Data

import gdal

#for one file:
modis_file = 'MOD10A1.A2009001.h09v05.005.2009009120443.hdf'
target_vector_file = file
g = gdal.Open(modis_file)

subdatasets = g.GetSubDatasets()
for fname, name in subdatasets:
    print name
    print "\t", fname
    
file_template = 'HDF4_EOS:EOS_GRID:"%s":MOD_Grid_Snow_500m:%s'
    
data_layer = 'MOD_Grid_Snow_500m:Fractional_Snow_Cover'

data ={}
for i,layer in enumerate(data_layer):
    this_file = file_template % (modis_file, layer)



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





