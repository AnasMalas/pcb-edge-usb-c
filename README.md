# PCB Edge USB C Connector Library
Use your PCB itself as a USB C connector! This repo includes a KiCAD and EasyEDA library containing 10, 14, and 24 Pin versions.

<p align="center">  <img src="media/PCB_Type_C.jpg"/>   </p>

Note: this is a female/port connector, you need to use a USB C cable with it. USB drives and cables have male/plug connectors.

For this footprint to work, your PCB must be 0.6 or 0.8 mm thick. I tested it with 0.6 mm, but later saw [a white paper from USB IF using 0.8 mm for a similar fully featured connector](https://www.usb.org/sites/default/files/USB4_Gen3_plug_HS_design_guide_white_paper_2020_10_27.pdf). 

This footprint is optimized to get the best of both worlds between following the spec and DFM. For example, the dogbone cutouts allow the right dimention at the tip of the plug, adding some much needed support. The slot width is made with PCB edge routing tolerance in mind, and silkscreen adds a layer of protection against the small ground pins found on the inner tip of plugs.

Add a thin layer of metal on both sides to get the silkscreen area to 1.2 mm thick to better support and strengthen the connector.

## Testing and usecases
One of the main use case of such a connector is for ports that will be used a handful of times, such as an MCU debug port. Another use case is when the PCB assembly needs to be impossibly thin while USB is not in use, such as [a USB powered business card](https://www.linkedin.com/posts/anasmalas_its-almost-time-im-very-excited-to-be-activity-7377190388052332545-6JOr/), and it might be a valid choice for ultra cheap toys or gadgets like tiny USB PCB flashlights.

USB C is an extremely reliable connector. With this footprint, we throw that out of the window. Instead of tens of thousands of mating cycles, this connector may sustain tens to hundreds of insertions with ENIG plating before the traces wear through or peel off, depending on the PCB process. While this may be better with hard gold, the internal latch will wear the fiberglass enough that the cable might not stay in place. This is not a reliability focused connector.

Do not use this for a frequently accessed or important connector like the main battery charging port, it is not reliable enough.

Some tests were done to verify the ability of this connector, photos and videos can be found in Media. Here are some highlights

### Contact wear
One mating cycle
<p align="center">  <img src="media/single_insertion_wear_contacts.jpg"/>   </p>
<p align="center">  <img src="media/single_insertion_wear_contacts_3.jpg"/>   </p>

100 mating cycles without power, 5 mating cycles at 6V 5A (resistive load with long leads), and 5 mating cycles at 20V 1.5A
<p align="center">  <img src="media/110_insertion_wear_contacts_5.jpg"/>   </p>
<p align="center">  <img src="media/110_insertion_wear_contacts_11.jpg"/>   </p>

### Latch wear
After one mating cycle
<p align="center">  <img src="media/single_insertion_wear_latch.jpg"/>   </p>

After 110 mating cycles, there is significant wear and the cable holds its place but is easy to unlatch. Note that the latch may be grounded, so by wearing into the side of the board, it might come in contact with inner planes. It would be better to not allow power planes near the latch edges.
<p align="center">  <img src="media/110_insertion_wear_latch.jpg"/>   </p>

### Bend and break
Side to side and twisting movement is very minimal. Without the metal shell or the additional midplane thickness, there is a lot of "up and down" movement possible.
<p align="center">  <img src="media/flex_test.jpg"/>   </p>

0.1 Nm is enough to snap this connector on the tested 0.6 mm PCB, after significant deflection. Only some layers of the PCB break and the conenctor can still be inserted and removed (test can be seen in a video in Media)
<p align="center">  <img src="media/snap_test_torque.jpg"/>   </p>

Due to the top layer being intact, the port is still useable, but may need a cable flip
<p align="center">  <img src="media/snap_test_contact.jpg"/>   </p>

### Thermal
A 15 minute thermal soak test was ran at 5A after 100 mating cycles, and showed a temperature rise of 30-40 C. The cable used had an integrated LED display and an LDO, and the design used a PMOS that got warm too, so it is hard to isolate the thermal performance of this port.
<p align="center">  <img src="media/thermal_test_15_min_at_5a.JPG"/>   </p>

A video in the Media folder shows the moment the connector is disconnected without stopping the load. No significant heating is obvious on the individual traces
<p align="center">  <img src="media/thermal_test_15_min_at_5a_unplug.JPG"/>   </p>


## Import instructions

### KiCAD
To use this library in kicad, download the zip file, open the Plugin and Content Manager (PCM), click "Install from file" and choose the zip file.

### EasyEDA
To use this library in EasyEDA pro, import the .elibz files, or search the common library for "PCBTypeC_10P" or "PCBTypeC_14P" to add the symbol to your schematic.

### Other
Some other EDA tools like Altium support importing KiCAD footprints, and EasyEDA supports export to Altium and PADS. Double check against the same footprint in KiCAD or EasyEDA after import.
