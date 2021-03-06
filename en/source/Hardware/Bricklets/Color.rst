
:breadcrumbs: <a href="../../index.html">Home</a> / <a href="../../index.html#hardware">Hardware</a> / Color Bricklet
:shoplink: ../../../shop/bricklets/color-bricklet.html

.. include:: Color.substitutions
   :start-after: >>>substitutions
   :end-before: <<<substitutions

.. _color_bricklet:

Color Bricklet
==============

.. raw:: html

	{% tfgallery %}

	Bricklets/bricklet_color_tilted_[?|?].jpg           Color Bricklet
	Bricklets/bricklet_color_w_master_[100|600].jpg     Color Bricklet with Master Brick
	Bricklets/bricklet_color_horizontal_[?|?].jpg       Color Bricklet
	Bricklets/bricklet_color_in_action_[100|600].jpg    Color Bricklet in action
	Bricklets/bricklet_color_brickv_[100|].jpg          Color Bricklet in Brick Viewer
	Dimensions/color_bricklet_dimensions_[100|600].png  Outline and drilling plan

	{% tfgalleryend %}


Features
--------

* Measures color (RGB), color temperature and illuminance (16bit resolution each)
* Equipped with switchable LED for defined illumination and color temperature


.. _color_bricklet_description:

Description
-----------

The Color :ref:`Bricklet <primer_bricklets>` can be used to
extend the features of :ref:`Bricks <primer_bricks>` with the
capability to measure `color <https://en.wikipedia.org/wiki/Color>`__,
`color temperature <https://en.wikipedia.org/wiki/Color_temperature>`__ and
`illuminance <https://en.wikipedia.org/wiki/Illuminance>`__ of a light source.
Thus the Bricklet can measure the color of an object via its reflected light.
To create a defined illumination and color temperature the Bricklet is equipped 
with a API switchable LED.

The Bricklet can be used for many purposes, e.g. sorting of objects by their
color.

.. image:: /Images/Bricklets/bricklet_color_wavelength_chart_350.jpg
   :scale: 100 %
   :alt: Chart Responsivity / Wavelength
   :align: center
   :target: ../../_images/Bricklets/bricklet_color_wavelength_chart_600.jpg

The Sensor is equipped with color filters for the colors red, green and blue 
(RGB). In the chart above the responsivity of the sensor in the given color 
range is shown. Additional to the color information (RGB) a fourth value is 
measured called "clear value" (C). This is the sensors value without any color
filter. Each value of RGB and C is measured as 16bit value. From these sensor
values the Bricklet computes two additional values: illuminance and color 
temperature each with 16bit resolution.



Technical Specifications
------------------------

================================  ============================================================
Property                          Value
================================  ============================================================
Sensor                            TCS34725
Current Consumption               0.2mA (LED off), 5mA (LED on)
--------------------------------  ------------------------------------------------------------
--------------------------------  ------------------------------------------------------------
Dynamic Range                     3800000:1
Color Resolution (R,G,B,C)        16bit each (0-65535)
Color Temperature Resolution      16bit (0-65535)
Illuminance Resolution            16bit (0-65535)
--------------------------------  ------------------------------------------------------------
--------------------------------  ------------------------------------------------------------
Dimensions (W x D x H)            25 x 20 x 5mm (0.98 x 0.79 x 0.19")
Weight                            2g
================================  ============================================================


Resources
---------

* TCS3472 datasheet (`Download <https://github.com/Tinkerforge/color-bricklet/raw/master/datasheets/TCS34725.pdf>`__)
* Schematic (`Download <https://github.com/Tinkerforge/color-bricklet/raw/master/hardware/color-schematic.pdf>`__)
* Outline and drilling plan (`Download <../../_images/Dimensions/color_bricklet_dimensions.png>`__)
* Source code and design files (`Download <https://github.com/Tinkerforge/color-bricklet/zipball/master>`__)


.. _color_bricklet_test:

Test your Color Bricklet
------------------------

|test_intro|

|test_connect| (see picture below).

.. image:: /Images/Bricklets/bricklet_color_w_master_600.jpg
   :scale: 100 %
   :alt: Color Bricklet connected to Master Brick
   :align: center
   :target: ../../_images/Bricklets/bricklet_color_w_master_1200.jpg

|test_tab|
If everything went as expected you can now see the changing measured values 
depending on the illumination.

.. image:: /Images/Bricklets/bricklet_color_brickv.jpg
   :scale: 100 %
   :alt: Color Bricklet in Brick Viewer
   :align: center
   :target: ../../_images/Bricklets/bricklet_color_brickv.jpg

|test_pi_ref|


Usage and Configuration
-----------------------

The sensor of the Bricklet can be configured. Gain and integration time can
be changed. Dark environments need a higher gain or a longer integration time.
If you use long integration times the sensor will react slower. If you need fast
measurements use a high gain and short integration times.

The desired configuration depends on the application. Depending on the 
illumination and distance to the measured object other parameters have to be chosen.
The Brick Viewer can be used to find proper values.

If you want to use the Bricklet in sorting applications it should be mounted in 
a fixed distance, with a fixed source of light (e.g. the equipped LED) and 
it should also be protected from interfering light.

.. _color_bricklet_programming_interface:

Programming Interface
---------------------

See :ref:`Programming Interface <programming_interface>` for a detailed description.

.. include:: Color_hlpi.table
