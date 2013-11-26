Data-Download
=============

#Discharge Data
#Reading the data invloved using the 'Save as' function in the browser

file = 'files/data/delnorte.dat'
data = np.loadtxt(file,usecols=(2,3),unpack=True,dtype=str)
plt.plot(data[1].astype(float))
import datetime
ds = np.array(data[0][0].split('-')).astype(int)
year,doy = datetime.datetime(ds[0],ds[1],ds[2]).strftime('%Y %j').split()
#All of the above code taken directly from the course notes


#Temperature Data
#Reading the data invloved using the 'Save as' function in the browser

