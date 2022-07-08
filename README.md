# Raster---Rasterio
Rasterio

Save each band separately

````python

import os
import rasterio


 src = rasterio.open(wv_tif)
    for band in range(1, src.count):
        single_band = src.read(band)

        # get the output name
        out_name = os.path.basename(wv_tif)
        file, ext = os.path.splitext(out_name)
        name = file + "_" + "B" + str(band) + ".tif"
        out_img = os.path.join(folder, name)

        print(out_img + " done")

        # Copy the metadata
        out_meta = src.meta.copy()

        out_meta.update({"count": 1})

        # save the clipped raster to disk
        with rasterio.open(out_img, "w", **out_meta) as dest:
            dest.write(single_band,1)
            
```
