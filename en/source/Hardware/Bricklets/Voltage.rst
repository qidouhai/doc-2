
:breadcrumbs: <a href="../../index.html">Home</a> / <a href="../../index.html#hardware">Hardware</a> / Voltage Bricklet

.. include:: Voltage.substitutions
   :start-after: >>>substitutions
   :end-before: <<<substitutions

.. _voltage_bricklet:

Voltage Bricklet
================

.. raw:: html

	{% tfgallery %}

	Bricklets/bricklet_voltage_tilted_[?|?].jpg           Voltage Bricklet
	Bricklets/bricklet_voltage_vertical_[?|?].jpg         Voltage Bricklet
	Bricklets/bricklet_voltage_horizontal_[?|?].jpg       Voltage Bricklet
	Bricklets/bricklet_voltage_master_[100|600].jpg       Voltage Bricklet with Master Brick
	Bricklets/bricklet_voltage_brickv_[100|].jpg          Voltage Bricklet in Brick Viewer
	Dimensions/voltage_bricklet_dimensions_[100|600].png  Outline and drilling plan

	{% tfgalleryend %}

.. note::

 The Voltage Bricklet is discontinued and is no longer sold. The
 :ref:`Analog In Bricklet 2.0 <analog_in_v2_bricklet>` is the recommended
 replacement.


Features
--------

* Measures voltages up to 50V (DC)
* Output in 1mV steps (12bit resolution)


.. _voltage_bricklet_description:

Description
-----------

The Voltage :ref:`Bricklet <primer_bricklets>` can be used to
extend the features of :ref:`Bricks <primer_bricks>` by the
capability to measure voltages. The measurement range is 0-50V (DC).
The voltage can be read out directly in `Volt
<https://en.wikipedia.org/wiki/Volt>`__ without conversion.
With configurable events it is possible to react on changing
voltages without polling.


Technical Specifications
------------------------

================================  ============================================================
Property                          Value
================================  ============================================================
Sensor                            Fixed voltage divider with factor 0.0625
Current Consumption               1mA
--------------------------------  ------------------------------------------------------------
--------------------------------  ------------------------------------------------------------
Voltage                           0V - 50V (DC) in 1mV steps, 12bit resolution
--------------------------------  ------------------------------------------------------------
--------------------------------  ------------------------------------------------------------
Dimensions (W x D x H)            25 x 25 x 14mm (0.98 x 0.98 x 0.55")
Weight                            4g
================================  ============================================================


Resources
---------

* Schematic (`Download <https://github.com/Tinkerforge/voltage-bricklet/raw/master/hardware/voltage-schematic.pdf>`__)
* Outline and drilling plan (`Download <../../_images/Dimensions/voltage_bricklet_dimensions.png>`__)
* Source code and design files (`Download <https://github.com/Tinkerforge/voltage-bricklet/zipball/master>`__)


.. _voltage_bricklet_test:

Test your Voltage Bricklet
--------------------------

|test_intro|

|test_connect|.
Additionally connect a voltage source to the Bricklet.
For testing purposes we have connected a battery
(see picture below).

.. image:: /Images/Bricklets/bricklet_voltage_master_600.jpg
   :scale: 100 %
   :alt: Voltage Bricklet with Battery connected to Master Brick
   :align: center
   :target: ../../_images/Bricklets/bricklet_voltage_master_1200.jpg

|test_tab|
If everything went as expected you can now see the voltage in volt
and a graph that shows the voltage over time.

.. image:: /Images/Bricklets/bricklet_voltage_brickv.jpg
   :scale: 100 %
   :alt: Voltage Bricklet in Brick Viewer
   :align: center
   :target: ../../_images/Bricklets/bricklet_voltage_brickv.jpg

|test_pi_ref|


.. _voltage_bricklet_programming_interface:

Programming Interface
---------------------

See :ref:`Programming Interface <programming_interface>` for a detailed description.

.. include:: Voltage_hlpi.table
