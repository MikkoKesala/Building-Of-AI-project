# Project Title

Biodiversity mapping

## Summary

Biodiversity mapping plays a pivotal role in informed decision-making, sustainable management, and ecological conservation. Accurate maps of biodiversity hotspots provide essential information on the distribution and intensity of biodiversity across different regions.


## Background

Biodiversity mapping is a challenging task due to the complexity of biodiversity, which exists at multiple levels, including genetic, species, and ecosystem diversity. A significant challenge is the reliance on proxy variables derived from remote sensing data, as direct measurement of biodiversity is not feasible. Another limitation lies in the constraints of remote sensing technology for producing high-resolution biodiversity maps over extensive areas. However, such high-resolution maps are vital for sustainable forestry practices, as they enable the identification of areas suitable for minimal-impact logging and those requiring conservation. This project addresses these challenges by focusing on species diversity mapping with high accuracy. Using open-access, nationwide remote sensing data such as color-infrared orthophotos and canopy height models, the project estimates biodiversity at the individual tree level.

Remote sensing data
* Canopy height model
* Color-infrared orthophots


## How is it used?

The solution begins with identifying individual trees from the canopy height model using commonly employed tree detection algorithms. This initial step allows for the accurate delineation of tree structures within the forest. The next phase involves enriching the identified tree data with color-infrared information, which provides valuable insights into tree species. The enriched data is then subjected to GIS-statistical analysis, which examines the surrounding areas within a specified radius. The output of GIS-statistical are used as input for the neural network model.

<img src=/Hotspot.PNG width="300">

Here is an example solution of the biodiversity mapping:
```
import numpy as np
def hidden_activation(z):
    return np.maximum(0.0,z)

def output_activation(z):
    return z

def biodiversity():
   
    proxies = ['geostat_height','geostat_ndvi','geostat_r','geostat_g','geostat_b']
   
    w0 = np.array([[ 0.51, 0.551 ],
                   [2.24, 2.53],
                   [4.21, 4.252],
                   [-2.42, -2.411],
                   [-3.53, -3.523]])
   
    w1 = np.array([[6.2 , 5.12],
                   [-0.432,  0.421]])
    w2 = np.array([[4.6],
                   [5.64]])
    b0 = np.array([-1.24, -0.41])
    b1 = np.array([-2.15, -1,252]) 
    b2 = np.array([-4.24])

    p_test = [[2.4,0.32,0.9,0.12,-0.23]]
    biod = []
    for p in p_test:
        h1_in = np.dot(p,w0) + b0
        h1_out = hidden_activation(h1_in)
    
        h2_in = np.dot(h1_out,w1) + b1
        h2_out = hidden_activation(h2_in)

        h3_in = np.dot(h2_out,w2) + b2
        out = output_activation(h3_in)
    
        biod.append(out)

    return biod
```
## Data sources and AI methods


| Data      | Description |
| ----------- | ----------- |
| Canopy height model      | https://avoin.metsakeskus.fi/rajapinnat/v1/CHM_newest/ows|
| Color-infrared   | https://avoin-karttakuva.maanmittauslaitos.fi/ortokuvat-ja-korkeusmallit/wcs/v2?  |
| Height | extracted from canopy height model |
| NDVI | extracted from color-infrared |
| geostat_height | extracted from height |
| geostat_ndvi | extracted from ndvi |
| geostat_[r/g/b] | extracted from color-infrared |

## Challenges

in progress

## What next?

in progress

## Acknowledgments

in progress
