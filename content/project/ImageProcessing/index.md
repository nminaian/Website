---
title: Computer Vision-based Fluid-Structure Interaction Tracking Software
summary: Developed a user interactive notebook within Wolfram Mathematica that can track object deflection, travel velocity, and particle tracking of acquired videography related to IPMC underwater sensor data.

tags:
- Computer Vision
- IPMC
date: "2020-11-25T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption:
  focal_point: Smart

links:
- icon: microscope
  icon_pack: fas
  name: Visit our Lab Website
  url: https://www.kwangjinkim.org/
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---

Project Scope

Ionic polymer-metal composites (IPMCs) are a type of electroactive polymer typically used in soft-robotic applications.The unique two-way transduction property of IPMCs allows for both actuation and sensing, which, in conjunction with its ability to be used in aqueous environments, can be used for various underwater applications. For this study, we aim to use the IPMC' s unique sensing capabilities as an underwater flow sensor, capable of measuring the flow field of the surrounding environment. This approach is dependent on signal characterization of the acquired voltage response and the fluid dynamics phenomenon of Kármán vortex streets. The latter requires the sensor to detect the frequency of vortex shedding from either the sensor itself or from an obstructing object positioned before the IPMC sensor. The project was split into three major goals : 1) Capture and track the relative velocity of IPMC sensor using imaging and image process techniques.Confirm this value with our known value, and calculate expected vortex shedding frequency with this velocity.2) Capture and and measure the tip displacement of the IPMC sensor during travel using imaging and image process techniques, and compare to acquired voltage data from the sensor.3) Capture and display shed vortices from the experiment.

Ionic Polymer-Metal Composites: An Overview

IPMCs are unique electroactive polymers in that they exhibit both electromechanical (electrical to mechanical) and mechanoelectrical (mechanical to electrical) transduction, like that of piezoelectric materials, and are constructed from flexible polymers that can sustain large deformations and strains . The core structure of an IPMC is an ionomeric-polymer (ionomer), which consists of strong ionic groups attached to a charge-neutral polymer backbone. With this ionomer structure, the IPMC is formed by compositing an electrode material, typically a noble metal (such as platinum, gold, palladium, or silver), onto the surface of a thin ionomer membrane.  This process forms the final material, a combined structure of an ionomer and metal electrodes, forming an ionic polymer-metal composite. The choice of backbone ionomer, electrode material, mobile ion species, solvent, and hydration level all have an immense impact on the behavior and performance of IPMC materials, demonstrating their highly complex nature. Regarding IPMCs as a sensor, induced deformation is believed to cause a redistribution of cations within the porous network due to mobility in the solvent, in addition to the anion-clusters deforming with the material such that the clusters form effective dipoles which induce a detectable signal along the electrodes, often within the millivolt range. The work presented herein will be focused on this aspect of IPMC physics.

Principles of Flow Sensing

One of the more prominent uses of IPMC sensors in underwater applications has been in the development of IPMC-based flow sensor devices. There have been two approaches in this endeavor, one of which involves interpreting the characteristic response directly, and the other requiring additional signal processing within the frequency domain.  The former is dependent relating the acquired voltage response directly to the environmental causes of displacement surrounding the IPMC. The figure below is a still-frame of an oscillating IPMC due to a shaker at 10 Hz.

Experimental Setup
Equipment
Experiments were conducted within an 85 gal aquarium with the IPMC sensor mounted to an inverted linear belt slide system (MacronDynamics MSA-M6S) driven by an stepper motor (Applied Motion Products SSM23IP-4EG). The motor software was programmed to run at 200 rps, traveling at 150 mm/rev (300 mm/s). Voltage readings were acquired directly using a Keithley 6510 DAQ. Three cameras were used for three individual applications: velocity, tip deflection, and particle tracking.

Camera 1: Velocity (Canon EOS Rebel SL1)
Fixed directly facing the side wall of the aquarium, camera 1 will be capturing the travel of the sensor mount. The camera is fitted with the stock 18-55mm Canon lens. Video was captured at 1080p, 30 fps. The far-side of the aquarium is fitted with a 1 inch grid poster that will be used when determining the calibration factor of the footage. Various light-sources were set behind the background image in order to produce a backlit, silhouette-esq footage of the sensor mount traveling.

Camera 2: Tip Deflection (OSMO Action)
Camera 2 was mounted directly to the carriage to travel alongside the sensor, directly observing sensor deformation from an above view. Camera 2 will be used to  relate the dynamic tip displacement of the IPMC to the acquired voltage response. Camera 2 captured high speed footage at 1080p, 240 fps, ideally to capture the nuance in the deformation.

Camera 3: Particle Tracking (GoPro Hero4 Session)
Camera 3 was placed at a fixed location on the floor of the aquarium where it was used to capture the life cycle of the shed vortices from the carriage/bluff body. The camera was set to capture footage at 1080p, 30 fps. In addition, to better visualize the vortices, packing foam was shredding into pieces, ultimately functioning as tracking particles which assisted in image processing the flow trends on the surface of the water.

Implementing Mathematica
Velocity Tracking
In this section, Mathematica was implemented to detect the velocity of a discrete binarized section of the sensor carriage mount. The found velocity can then be used in calculating the expected frequency of vortex shedding and can be used to verify the set velocity from the provided linear belt slide software. An assumption is made that the carriage, clamp, and IPMC sensor are traveling as a single body, and thus share the same velocity.  Prior to analysis, the captured experimental video was exported as a series of .png images through an external video editing software, which was then imported into Mathematica in the following cells. The images must be resized due to the large quantity. The spatial calibration factor was determined using the 1" grid background, which is highlighted in the first image shown.

A mask was applied to isolate a specific region of capture that will be used for simplifying the binarization of the moving carriage. With the mask applied, the series of images were then color separated into CMYK color channels. The yellow channel, which best isolated the color of the clamp, was used to easily identify the moving carriage using a threshold binarization.  The ComponentMeasurements function was then applied to determine the centroid of the binarized component within each frame. The "centroids" variable was specifically used for velocity measurement, while "centroid" was used for highlighting the carriage in the tracking animation.

A list of velocities were then established by determining distance travel in successive frames and then by subsequently dividing the time step and and multiplying by the calibration factor. A "0" value was appended to the velocity list to account for the carriage exiting the FOV at the final frame. A mean velocity was then calculated by partitioning a stable region of velocities. The results were then plotted using ListLinePlot.

IPMC Displacement Tracking
The following section of code is used to track IPMC deformation during travel. Similar to the first portion of code, images of gathered experimental footage were imported and resized for data management. Prior to binarization, a mask was applied to each frame to isolate the region of interest. Due to difficulty in binarization, a specific range of frames were chosen where the binarization was found to be the most stable. During binarization, a Sobel edge detection kernel was applied to increase accuracy of binarization by detecting the edge of the rectangular IPMC. A second mask was then applied to segment the IPMC into four sections for tracking curvature. There was difficulty in binarizing this set of footage due to the reflection of the water and almost near transparency of the IPMC. It may be useful to attempt to make the points of interest more prominent during experimental imaging for better clarity and accuracy during binarization. The ComponentMeasurement feature was then used to determine the centroids of each segmented section of the IPMC during travel.

Displacement was calculated by determining the distance traveled by the centroid of successive frames. The centroid of each component was then plotted which reveals the effects of curvature, as the furthest points from the clamp have the highest amplitude. This displacement plot was also compared to the voltage response acquired from the IPMC directly using a data acquisition device. These two plots show very similar trends.

Particle Tracking
In this section, pseudo-PIV images were obtained to show flow patterns over time at a fixed location. Experimental images were imported and resized for data management. A local adaptive binarize was used in order to identify particles. The experiment setup created limitations in isolating particles during binarization and thus environmental objects are seen in binarized images. This will in turn affect the accuracy of flow pattern analysis. Having particles that are dissimilar to the environment can potentially allow for better tracking and flow pattern analysis.

An example of partitioning a frame to determine displacements of each section of a single image. An image correlate was used to determine these displacement vectors. Once these displacement vectors were found an animation was made of the binarized images with an overlay of the displacement vectors.

Final code below for determining the flow field. This code was found in Lecture 23 of ME 695.

Future Work
Some improvements to the work presented herein include increasing the quality of imaging during the experimental process. This includes establishing a better lighting system, applying more prominent tracking points, and providing an in-plane measurement tool for more precise distance calibration. In the particle tracking experiment, providing a dark backdrop for better particle observation would allow for ease of image processing. Lastly, using the Hough transform function in Mathematica could improve on the IPMC deformation tracking. An example of this is shown below from a modified MATLAB documentation code regarding Hough transformations.