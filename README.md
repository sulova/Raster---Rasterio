# Raster---Rasterio
Rasterio

Save each band separately

````python

import os
import rasterio

a = [ "B2_p10", "B2_p20", "B2_p50", "B2_p90", "B2_p95", "B12_p10", "B12_p20", "B12_p50" , "B12_p90" , "B12_p95" ,
             "B8_p10", "B8_p20", "B8_p50", "B8_p90", "B8_p95", "B6_p10",  "B6_p20", "B6_p50", "B6_p90", "B6_p95"] 

src = rasterio.open('../Data/Tree_Heights/S2.tif')
for band in range(1, src.count):
        single_band = src.read(band)

        # get the output name
        out_name = os.path.basename('../Data/Tree_Heights/S2.tif')
        file, ext = os.path.splitext(out_name)
        name = file + "_" + a[band] + ".tif"
        out_img = os.path.join('../Data/Tree_Heights/', name)

        print(out_img + " done")

        # Copy the metadata
        out_meta = src.meta.copy()

        out_meta.update({"count": 1})

        # save the clipped raster to disk
        with rasterio.open(out_img, "w", **out_meta) as dest:
            dest.write(single_band,1)
            
```
