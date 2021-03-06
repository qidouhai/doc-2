
:breadcrumbs: <a href="../index.html">Home</a> / <a href="../index.html#software-perl">Software</a> / Perl - IP Connection

.. |ref_api_bindings| replace:: :ref:`Perl API bindings <api_bindings_perl>`
.. |ref_install_guide| replace:: :ref:`installation guide <api_bindings_perl_install>`
.. |bindings_name| replace:: Perl

.. _ipcon_perl:

Perl - IP Connection
======================

.. include:: IPConnection_Common.substitutions
   :start-after: >>>intro
   :end-before: <<<intro


.. _ipcon_perl_examples:

Examples
--------

The example code below is `Public Domain (CC0 1.0)
<http://creativecommons.org/publicdomain/zero/1.0/>`__.

Enumerate
^^^^^^^^^

`Download (example_enumerate.pl) <https://github.com/Tinkerforge/generators/raw/master/perl/example_enumerate.pl>`__

.. literalinclude:: IPConnection_Perl_example_enumerate.pl
 :language: perl
 :linenos:
 :tab-width: 4


Authenticate
^^^^^^^^^^^^

`Download (example_authenticate.pl) <https://github.com/Tinkerforge/generators/raw/master/perl/example_authenticate.pl>`__

.. literalinclude:: IPConnection_Perl_example_authenticate.pl
 :language: perl
 :linenos:
 :tab-width: 4


.. _ipcon_perl_api:

API
---

Generally, every subroutine of the Perl bindings can report an error as
``Tinkerforge::Error`` object via ``croak()``. The object has a
``get_code()`` and a ``get_message()`` subroutine. There are different
error code:

* Error->ALREADY_CONNECTED = 11
* Error->NOT_CONNECTED = 12
* Error->CONNECT_FAILED = 13
* Error->INVALID_FUNCTION_ID = 21
* Error->TIMEOUT = 31
* Error->INVALID_PARAMETER = 41
* Error->FUNCTION_NOT_SUPPORTED = 42
* Error->UNKNOWN_ERROR = 43

All methods listed below are thread-safe.

Basic Functions
^^^^^^^^^^^^^^^

.. perl:function:: IPConnection->new()

 Creates an IP Connection object that can be used to enumerate the available
 devices. It is also required for the constructor of Bricks and Bricklets.


.. perl:function:: IPConnection->connect($host, $port)

 :param $host: string
 :param $port: int
 :rtype: undef

 Creates a TCP/IP connection to the given ``$host`` and ``$port``. The host and port
 can refer to a Brick Daemon or to a WIFI/Ethernet Extension.

 Devices can only be controlled when the connection was established
 successfully.

 Blocks until the connection is established and throws an exception if there
 is no Brick Daemon or WIFI/Ethernet Extension listening at the given
 host and port.


.. perl:function:: IPConnection->disconnect()

 :rtype: undef

 Disconnects the TCP/IP connection from the Brick Daemon or the WIFI/Ethernet
 Extension.


.. perl:function:: IPConnection->authenticate($secret)

 :param $host: string
 :rtype: undef

 Performs an authentication handshake with the connected Brick Daemon or
 WIFI/Ethernet Extension.
 If the handshake succeeds the connection switches from non-authenticated to
 authenticated state and communication can continue as normal. If the handshake
 fails then the connection gets closed. Authentication can fail if the wrong
 secret was used or if authentication is not enabled at all on the Brick Daemon
 or the WIFI/Ethernet Extension.

 See the :ref:`authentication tutorial <tutorial_authentication>` for more
 information.

 .. versionadded:: 2.1.0


.. perl:function:: IPConnection->get_connection_state()

 :rtype: int

 Can return the following states:

 * IPConnection->CONNECTION_STATE_DISCONNECTED (0): No connection is established.
 * IPConnection->CONNECTION_STATE_CONNECTED (1): A connection to the Brick Daemon
   or the WIFI/Ethernet Extension  is established.
 * IPConnection->CONNECTION_STATE_PENDING (2): IP Connection is currently trying
   to connect.


.. perl:function:: IPConnection->set_auto_reconnect($auto_reconnect)

 :param $auto_reconnect: bool
 :rtype: undef

 Enables or disables auto-reconnect. If auto-reconnect is enabled,
 the IP Connection will try to reconnect to the previously given
 host and port, if the currently existing connection is lost.
 Therefore, auto-reconnect only does something after a successful
 :perl:func:`connect() <IPConnection->connect>` call.

 Default value is 1.


.. perl:function:: IPConnection->get_auto_reconnect()

 :rtype: bool

 Returns 1 if auto-reconnect is enabled, 0 otherwise.


.. perl:function:: IPConnection->set_timeout($timeout)

 :param $timeout: float
 :rtype: undef

 Sets the timeout in seconds for getters and for setters for which the
 response expected flag is activated.

 Default timeout is 2.5.


.. perl:function:: IPConnection->get_timeout()

 :rtype: float

 Returns the timeout as set by :perl:func:`set_timeout() <IPConnection->set_timeout>`.


.. perl:function:: IPConnection->enumerate()

 :rtype: undef

 Broadcasts an enumerate request. All devices will respond with an enumerate
 callback.


Callback Configuration Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. perl:function:: IPConnection->register_callback($callback_id, $function)

 :param $callback_id: int
 :param $function: string
 :rtype: undef

 Registers the given ``$function`` name with the given ``$callback_id``.

 The available callback IDs with corresponding function signatures
 are described below.


Callbacks
^^^^^^^^^

Callbacks can be registered to be notified about events. The registration is
done with the :perl:func:`register_callback() <IPConnection->register_callback>`
function. The first parameter is the callback ID and the second
parameter the callback function:

.. code-block:: perl

    sub my_callback
    {
        print "@_[0]";
    }

    $ipcon->register_callback(IPConnection->CALLBACK_EXAMPLE, 'my_callback')

The callback function will be called from an internal thread of the
IP Connection. In contrast to many other programming languages, variables are
not automatically shared between threads in Perl. If you want to share a global
variable between a callback function and the rest for your program it has to be
marked as ``:shared``. See the documentation of the `threads::shared
<http://perldoc.perl.org/threads/shared.html>`__ Perl module for more details.

The available constants with inherent number and type of parameters are
described below.


.. perl:attribute:: IPConnection->CALLBACK_ENUMERATE

 :param $uid: string
 :param $connected_uid: string
 :param $position: char
 :param @hardware_version: [int, int, int]
 :param @firmware_version: [int, int, int]
 :param $device_identifier: int
 :param $enumeration_type: int

 The callback has seven parameters:

 * ``$uid``: The UID of the device.
 * ``$connected_uid``: UID where the device is connected to. For a Bricklet this
   will be a UID of the Brick where it is connected to. For a Brick it will be
   the UID of the bottom Master Brick in the stack. For the bottom Master Brick
   in a stack this will be "0". With this information it is possible to
   reconstruct the complete network topology.
 * ``$position``: For Bricks: '0' - '8' (position in stack). For Bricklets:
   'a' - 'd' (position on Brick).
 * ``@hardware_version``: Major, minor and release number for hardware version.
 * ``@firmware_version``: Major, minor and release number for firmware version.
 * ``$device_identifier``: A number that represents the device.
 * ``$enumeration_type``: Type of enumeration.

 Possible enumeration types are:

 * IPConnection->ENUMERATION_TYPE_AVAILABLE (0): Device is available
   (enumeration triggered by user: :perl:func:`enumerate()
   <IPConnection->enumerate>`). This enumeration type can occur multiple times
   for the same device.
 * IPConnection->ENUMERATION_TYPE_CONNECTED (1): Device is newly connected
   (automatically send by Brick after establishing a communication connection).
   This indicates that the device has potentially lost its previous
   configuration and needs to be reconfigured.
 * IPConnection->ENUMERATION_TYPE_DISCONNECTED (2): Device is disconnected
   (only possible for USB connection). In this case only ``$uid`` and
   ``$enumeration_type`` are valid.

 It should be possible to implement plug-and-play functionality with this
 (as is done in Brick Viewer).

 The device identifier numbers can be found :ref:`here <device_identifier>`.
 There are also constants for these numbers named following this pattern::

  <device-class>->DEVICE_IDENTIFIER

 For example: :perl:attr:`BrickMaster->DEVICE_IDENTIFIER`
 or :perl:attr:`BrickletAmbientLight->DEVICE_IDENTIFIER`.


.. perl:attribute:: IPConnection->CALLBACK_CONNECTED

 :param $connect_reason: int

 This callback is called whenever the IP Connection got connected to a
 Brick Daemon or to a WIFI/Ethernet Extension, possible reasons are:

 * IPConnection->CONNECT_REASON_REQUEST (0): Connection established after
   request from user.
 * IPConnection->CONNECT_REASON_AUTO_RECONNECT (1): Connection after
   auto-reconnect.


.. perl:attribute:: IPConnection->CALLBACK_DISCONNECTED

 :param $disconnect_reason: int

 This callback is called whenever the IP Connection got disconnected from a
 Brick Daemon or from a WIFI/Ethernet Extension, possible reasons are:

 * IPConnection->DISCONNECT_REASON_REQUEST (0): Disconnect was requested by user.
 * IPConnection->DISCONNECT_REASON_ERROR (1): Disconnect because of an
   unresolvable error.
 * IPConnection->DISCONNECT_REASON_SHUTDOWN (2): Disconnect initiated by Brick
   Daemon or WIFI/Ethernet Extension.
