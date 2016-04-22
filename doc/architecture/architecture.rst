.. _architecture:

Ostro |trade| OS Architecture
#############################

Introduction
============

The Ostro |trade| OS is a pre-compiled, configured and secured base
Internet of Things (IoT) Linux\* OS that supports creating custom images
easily. For more information, see :ref:`about_ostro`.

This document gives an overview to Ostro OS architecture and the basic
building blocks. Furthermore, the document briefly talks about how
Ostro OS meets different end-user use-cases ranging from hacking to
IoT product creation.

.. _`Yocto Project`: http://yoctoproject.org
.. _`Soletta Project`: http://solettaproject.org
.. _`Node.JS`: https://nodejs.org
.. _`IoTivity`: https://www.iotivity.org/

Ostro |trade| OS Characteristics
=================================

In Ostro |trade| OS, there are four key characteristics that
drive the architecture design:

1. Ostro OS uses standard libraries and services: The building blocks
used in Ostro OS are commonly used in open source and any Ostro OS
custom implementation is avoided. This has a big benefit because it
means there is no extra porting/platform adaptation needed to get
existing applications or services run in Ostro OS.

2. Ostro OS is pre-compiled and configured: Ostro OS is based
on the `Yocto Project_` and is provided
as pre-compiled and configured distribution for IoT. There is no
end-user compilation needed when starting from scratch with Ostro OS
since the build system is configured to use the shared. In addition,
pre-compiled reference images are available for download.

3. Ostro OS is secured and built with security in mind: Security is
critical for IoT and it is also a focus in Ostro OS. The security
design is to provide scalable options how security can be configured
in Ostro based products. The security architecture is explained in
more details in :ref: `system-and-security-architecture`.

4. Ostro OS is easy to customize: While Ostro OS comes pre-compiled
(binaries and images), it is important that the OS can be customized
to meet the diverse product needs in IoT space. With the help of
Yocto Project build system used by Ostro OS, it is easy to customize
the build and images to suit the needs. :ref:`quick_start/about` and
the links provided there give a good start to Ostro OS customization.

Ostro |trade| OS Architecture Stack
===================================

One way to descibe Ostro OS architecture is to build a stack from
hardware platform up to an IoT Application layer. This stack is
illustrated in Fig 1.

.. image::images/ostro_os_architecture.png

In the following, each layer is explained in more detail.

IoT Applications
----------------
The IoT applications layer consist of all applications that use the
underlying platform. Ostro OS itself currently does not
implement any concrete IoT use-cases via applications but many sample
applications are provided to demonstrate the OS services.

Programming Interfaces
-----------------------
Ostro OS provides various application runtimes to allow the end-user
more choices to use in their IoT applications.

* `Soletta Project`_ is an open source
framework for making IoT applications. The project provides libraries
to make it quick and easy to write software for IoT devices. The
applications can we written using a flow-based programing (FBP) or
more traditionally as C applications linking to Soletta's C based
platform APIs.

* `Node.JS`_ is a popular JavaScript runtime to
run (IoT) web applications. Ostro OS provides the Node.JS runtime
and selected JavaScript APIs (as Node.JS modules) to build IoT
applications. The set of APIs include, e.g., a Javascript API for
the OIC specification. The Javascript API set is kept aligned with
the API set provided by Soletta.

* In addition to Soletta and Node.JS, common programming languages/
runtimes in IoT space are supported. Ostro OS provides Python runtime
and Java Platform (OpenJDK8) that are popular in the IoT space.

Frameworks
----------

Frameworks provide an abstraction to platform services. For making
application deployment easy, the Ostro Application
Framework :ref:`application_framework` provides tooling for
application writers to get the applications running in an Ostro OS
based image.

The Ostro Application framework implements a systemd generator that
parses the application manifest files to systemd .service.

`IoTivity`_ TODO

Services
--------

The responsibility of system services is to bring up the system,
manage wireless connections, and process' IPC. The components
used are commonly used in all open source OSes: systemd, connman,
bluez, and D-Bus.

In addition to systemd and connectivity, Ostro OS comes with
:ref: `software-update` technology that helps to support software
updates to deployed devices.

Base Libraries
--------------

Standard Linux base libraries are used in Ostro...


Linux Kernel and Hardware Adaptation
-------------------------------------

The hardware BSPs for Ostro OS run the Linux Kernel. The kernel
provides the necessary drivers and hardware adaptation.

Sensors and connectivity are critical for IoT devices. Therefore,
Ostro OS maintains a dedicated page: :ref: `hardware` that describes
how various peripherals can be run with :ref:`quick_start/platforms`

Ostro |trade| OS Composition
=============================

The Ostro OS is a composition of multiple Yocto Project build system
metadata maintained in individual layer repositories. The layers used
in Ostro OS are composed into `ostro-os`.

The following layer repositories are used in Ostro OS. The Board
Support Package (BSP) layers

========================= =======================================
Layer Description
========================= =======================================
openembedded-core         Core metadata and major source of
                          all component recipes
meta-appfw                Ostro OS application framework recipes
meta-intel-iot-middleware Middleware components used in Intel IoT
                          DevKit
meta-intel-iot-security   Security building blocks: IMA, SMACK.
meta-iotqa                Ostro OS test tools
meta-iot-web              Layer for Node.JS and some JavaScript
                          APIs
meta-java                 Java support (openjdk8)
meta-oic                  IoTivity
meta-ostro                Ostro OS distro metadata, configuration,
                          and documentation
meta-ostro-bsp            Ostro OS BSP configuration metadata
meta-ostro-fixes          Ostro OS layer that is used to carry
                          fixes to upstream layers
meta-security-isafw       Image Security Analysis framework gives
                          offline tooling to analyze images
meta-soletta              Soletta Project
meta-swupd                Software update tooling
meta-intel                BSP layer for common IA platforms
meta-yocto-bsp            BSP layer for beaglebone black
meta-edison-bsp           BSP layer for Intel Edison.
========================= =======================================

TBD: Ostro |trade| OS Development Workflows
======================================

* eSDK
* swupd feeds
* SSTATE

Ostro |trade| OS Technical Documentation
=======================================

The following documents give more technical details about Ostro
|trade| OS components and their usage.

.. toctree::
   :maxdepth: 1

   disk-layout
   efi-boot
   software-update
   application-framework
   security-threat-analysis
   system-and-security-architecture

