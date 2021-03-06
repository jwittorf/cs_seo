﻿.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _extend-sitemap:

Extend the Sitemap.xml
----------------------

The sitemap.xml generation in cs_seo is very flexible. Here is shown how to extend the sitemap.xml for extensions and with external sitemaps.

.. _extend-sitemap-news-ts:

Add TypoScript for news
^^^^^^^^^^^^^^^^^^^^^^^

Include the TypoScript from cs_seo called "Sitemap.xml for News". The reference you'll find here: :ref:`sitemap.xml.news`.


.. _extend-sitemap-records-ts:

Add TypoScript for records
^^^^^^^^^^^^^^^^^^^^^^^^^^

To add records from your own extension you can easily add the following TypoScript.

::

    # default configuration to show a sitemap.xml for tx_news records #
    plugin.tx_csseo.sitemap {
		extensions {
			# configuration for an extension, the name is an identifier
			myext {
				# string; the table name where the records are stored
				table = tx_myext_domain_model_entry

				# string; will be attached to the typolink, more params are possible, the last one is the record param
				additionalParams = tx_myext_pi1[controller]=Entry&tx_myext_pi1[action]=show&tx_myext_pi1[entry]

				# boolean; use cHash on url creation
				useCacheHash = 1

				# string; add custom query options : title LIKE '%top%'
				additionalWhereClause =

				# comma separated list; page uid where the records are stored
				storagePid =

				# int; extend the storage pid by a recursive level
				recursive =

				# int; page uid where the details are shown
				detailPid =

				# comma separated list; configure the available languages, e.g.: 0,1
				languageUids =

				# comma separated list; display only records with this categories
				categories =

				# string; if categories were saved in the same table, set here the field name
				categoryField =

				# string; if categories were saved in a MM-Table set here the name of the table
				categoryMMTable = sys_category_record_mm

				# boolean; true if the MM table has a column 'tablenames' which contains the current record table
				categoryMMTablenames = 1

				# string; if set the column 'fieldname' of the MM-table must be this
				categoryMMFieldname = categories

				# string; set here the name of the category table, required if you use the categoryDetailPidField
				categoryTable = sys_category

				# string; if set the detailPid will be overwritten if the category of a record has a field with this name and this field is not empty
				categoryDetailPidField = single_pid

				# string; If set the user function is called to fetch the records for the sitemap. The configuration is passed to the user function.
				getRecordsUserFunction = Vendor\MyExt\UserFunction\CsSeoSitemap->getMyRecords
			}
		}
	}

.. _extend-sitemap-additional-ts:

Add more external sitemaps
^^^^^^^^^^^^^^^^^^^^^^^^^^

It is possible to add custom sitemaps via TypoScript:

::

	plugin.tx_csseo.sitemap {
		additional {
			# addition external sitemaps:
			10 = https://mysite.com/sitemap-blog.xml
		}
	}
