:orphan:

.. _whats_new:

.. currentmodule:: mne_bids

What's new?
===========

.. _changes_0_17:

Version 0.17 (unreleased)
-------------------------

👩🏽‍💻 Authors
~~~~~~~~~~~~~~~

The following authors contributed for the first time. Thank you so much! 🤩

* `Christian O'Reilly`_
* `Berk Gerçek`_
* `Arne Gottwald`_
* `Matthias Dold`_

The following authors had contributed before. Thank you for sticking around! 🤘

* `Stefan Appelhoff`_
* `Daniel McCloy`_
* `Scott Huberty`_
* `Pierre Guetschel`_

Detailed list of changes
~~~~~~~~~~~~~~~~~~~~~~~~

🚀 Enhancements
^^^^^^^^^^^^^^^

- :func:`mne_bids.write_raw_bids()` can now handle mne `Raw` objects with `eyegaze` and `pupil` channels, by `Christian O'Reilly`_ (:gh:`1344`)
- :func:`mne_bids.get_entity_vals()` has a new parameter ``ignore_suffixes`` to easily ignore sidecar files, by `Daniel McCloy`_ (:gh:`1362`)
- Empty-room matching now preferentially finds recordings in the subject directory tagged as `task-noise` before looking in the `sub-emptyroom` directories. This adds support for a part of the BIDS specification for ER recordings, by `Berk Gerçek`_ (:gh:`1364`)
- Path matching is now implemenented in a more efficient manner within :meth:`mne_bids.BIDSPath.match()` and :func:`mne_bids.find_matching_paths()`, by `Arne Gottwald` (:gh:`1355`)
- :func:`mne_bids.get_entity_vals()` has a new parameter ``include_match`` to prefilter item matching and ignore non-matched items from begin of directory scan, by `Arne Gottwald` (:gh:`1355`)
- Data from ``events.tsv`` can now be read into an OrderedDict using :func:`mne_bids.events_file_to_annotation_kwargs()`, by `Matthias Dold` (:gh:`1389`)
- Read the optionally present extra columns from ``events.tsv`` and pass them to :class:`mne.Annotations`, by `Pierre Guetschel` (:gh:`1401`)


🧐 API and behavior changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

- :func:`mne_bids.make_dataset_description` will now auto-generate basic ``GeneratedBy`` fields if ``generated_by=None``. To suppress the auto-generated fields, pass an empty list. By `Daniel McCloy`_ (:gh:`1384`)

🛠 Requirements
^^^^^^^^^^^^^^^

- MNE-BIDS now requires ``mne`` 1.8 or higher.

🪲 Bug fixes
^^^^^^^^^^^^

- :func:`mne_bids.read_raw_bids` can optionally return an ``event_id`` dictionary suitable for use with :func:`mne.events_from_annotations`, and if a ``values`` column is present in ``events.tsv`` it will be used as the source of the integer event ID codes, by `Daniel McCloy`_ (:gh:`1349`)
- BIDS dictates that the recording entity should be displayed as "_recording-" in the filename. This PR makes :class:`mne_bids.BIDSPath`  correctly display "_recording-" (instead of "_rec-") in BIDSPath.fpath. By `Scott Huberty`_ (:gh:`1348`)
- :func:`mne_bids.make_dataset_description` now correctly encodes the dataset description as UTF-8 on disk, by `Scott Huberty`_ (:gh:`1357`)
- Corrects extension when filtering filenames in :meth:`mne_bids.BIDSPath.match()` and :func:`mne_bids.find_matching_paths()`, by `Arne Gottwald` (:gh:`1355`)
- Fix :class:`mne_bids.BIDSPath` partially matching a value, by `Pierre Guetschel` (:gh:`1388`)

API changes
^^^^^^^^^^^

- Add ``format`` kwarg to :func:`write_raw_bids` that allows users to specify if they want to force conversion to ``BrainVision`` or ``FIF`` file format, by `Adam Li`_ (:gh:`672`)
- :func:`mne_bids.BIDSPath.fpath` does not infer a full filepath anymore if the ``suffix``, or ``extension`` is missing. It returns the file path defined by the existing entities, by `Adam Li`_ and `Alexander Gramfort`_ (:gh:`721`)

Requirements
^^^^^^^^^^^^

- For writing BrainVision files, ``pybv`` version 0.5 is now required to allow writing of non-voltage channels, by `Adam Li`_ (:gh:`670`)

Bug fixes
^^^^^^^^^

- Fix writing MEGIN Triux files, by `Alexandre Gramfort`_ (:gh:`674`)
- Anonymization of EDF files in :func:`write_raw_bids` will now convert recording date to ``01-01-1985 00:00:00`` if anonymization takes place, while setting the recording date in the ``scans.tsv`` file to the anonymized date, thus making the file EDF/EDFBrowser compliant, by `Adam Li`_ (:gh:`669`)
- :func:`mne_bids.write_raw_bids` will not overwrite an existing ``coordsystem.json`` anymore, unless explicitly requested, by `Adam Li`_ (:gh:`675`)
- :func:`mne_bids.read_raw_bids` now properly handles datasets without event descriptions, by `Richard Höchenberger`_ (:gh:`680`)
- :func:`mne_bids.stats.count_events` now handles files without a ``trial_type`` or ``stim_type`` column gracefully, by `Richard Höchenberger`_ (:gh:`682`)
- :func:`mne_bids.read_raw_bids` now correctly treats ``coordsystem.json`` as optional for EEG and MEG data, by `Diego Lozano-Soldevilla`_ (:gh:`691`)
- :func:`mne_bids.read_raw_bids` now ignores ``exclude`` parameters passed via ``extra_params``, by `Richard Höchenberger`_ (:gh:`703`)
- :func:`mne_bids.write_raw_bids` now retains original event IDs in the ``value`` column of ``*_events.tsv``, by `Richard Höchenberger`_ (:gh:`708`)
- Fix writing correct ``iEEGCoordinateSystemDescription``, by `Stefan Appelhoff`_ (:gh:`706`)
- FIF files that were split due to filesize limitations (using the ``_split-<label>`` entity), are now all listed in ``scans.tsv``, as recommended by BIDS, by `Eduard Ort`_ (:gh:`710`)

- Tests that were adding or deleting files to/from a session-scoped dataset now properly clean up after themselves, by `Daniel McCloy`_ (:gh:`1347`)

:doc:`Find out what was new in previous releases <whats_new_previous_releases>`

.. include:: authors.rst
