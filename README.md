# ArcGIS Online Bug - Map Viewer Classic does not load WMS Layer

## Bug description

When loading a WMS layer in MapViewer (classic), the viewer returns an exception.

`Access to XMLHttpRequest at 'https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms?SERVICE=WMS&REQUEST=GetCapabilities' from origin 'https://esrica-ncr.maps.arcgis.com' has been blocked by CORS policy: The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' when the request's credentials mode is 'include'. The credentials mode of requests initiated by the XMLHttpRequest is controlled by the withCredentials attribute.`

The WMS service used for this test case: https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms?service=WMS

This business case used to work on older versions of ArcGIS Online and ArcGIS Enterprise.

## Requirements

For this test cases you will need the following conditions:

 * Have an ArcGIS Online account
 * Be an administrator
 * Have access to  machine with IIS or a Web Server installed.

# Map Viewer Test Case

Log in your ArcGIS Online organization. In my case: https://esrica-ncr.maps.arcgis.com/

## Make sure your organization settings are setup correctly

In ArcGIS Online, go into your organization settings.
 * In the left menu, go into `Security`
 * Add the URL: https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms in `Trusted Servers`
 * Add the URL: https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms in `Allow Origins`


 ## Try loading the WMS in Map Viewer (Classic)

 Open the map viewer, and create a new map. In the map menu, do the following:

  * Select `Add`
  * Select `Add Layer from the web`
  * In the drop drown menu, select `A WMS OGC Service`
  * Copy and Paste the URL `https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms?service=WMS`

  ![AddWMSService](images/add-wms.png) 

If you open your browser in developer mode, you will see the following error in your Chrome browser. The error should be the following:

`Access to XMLHttpRequest at 'https://cwfis.cfs.nrcan.gc.ca/geoserver/public/wms?SERVICE=WMS&REQUEST=GetCapabilities' from origin 'https://esrica-ncr.maps.arcgis.com' has been blocked by CORS policy: The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' when the request's credentials mode is 'include'. The credentials mode of requests initiated by the XMLHttpRequest is controlled by the withCredentials attribute.`

![Add WMS Error](images/wms-error.png) 


# Try loading the WMS in the classic API's

Register the parent directory of this read me in IIS. In my case, I have added a virtual directory called `wms` that points to the location of this repository.

![Add WMSA Service](images/iis-wms.png) 


You can see that the WMS we used in the map viewer works fine with the API. We'have just taken defaut sample and pointed them to your WMS Service.

 * http://localhost/wms/3/
 * http://localhost/wms/4/ 


## http://localhost/wms/3/

![WMS Service JS3](images/sample-js3.png) 

The sample used for API 3 is coming from there. https://developers.arcgis.com/javascript/3/jssamples/layers_wmsresourceinfo.html. The initial sample has vanilla setting.

The same result can be observed when I use the same CORS setting than the ArcGIS Online viewer, so at least that cannot be the only culprit. The URL for testing that would be: http://localhost/wms/3-cors/

## http://localhost/wms/4/

![WMS Service JS4](images/sample-js4.png) 

Sample for WMS Layer using JS4: https://developers.arcgis.com/javascript/latest/sample-code/sandbox/?sample=layers-wms 








