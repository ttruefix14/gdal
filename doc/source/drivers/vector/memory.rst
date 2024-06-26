.. _vector.memory:

Memory
======

.. shortname:: Memory

.. built_in_by_default::

This driver implements read and write access layers of features
contained entirely in memory. This is primarily useful as a high
performance, and highly malleable working data store. All update
options, geometry types, and field types are supported.

There is no way to open an existing Memory datastore. It must be created
with CreateDataSource() and populated and used from that handle. When
the datastore is closed all contents are freed and destroyed.

The driver does not implement spatial or attribute indexing, so spatial
and attribute queries are still evaluated against all features. Fetching
features by feature id should be very fast (just an array lookup and
feature copy).

Driver capabilities
-------------------

.. supports_create::

.. supports_georeferencing::

Creation Issues
---------------

Any name may be used for a created datasource. There are no datasource
or layer creation options supported. Layer names need to be unique, but
are not otherwise constrained.

Before GDAL 2.1, feature ids passed to CreateFeature() are preserved
*unless* they exceed 10000000 in which case they will be reset to avoid
a requirement for an excessively large and sparse feature array.
Starting with GDAL 2.1, sparse IDs can be handled.

New fields can be added or removed to a layer that already has features.

Layer creation options
~~~~~~~~~~~~~~~~~~~~~~

|about-layer-creation-options|
The following layer creation options are available:

-  .. lco:: ADVERTIZE_UTF8
      :choices: YES, NO
      :default: NO

      Whether the layer will contain UTF-8 strings.

-  .. lco:: FID
      :choices: <string>
      :default: empty string
      :since: 3.8

      Name of the FID column to create.
