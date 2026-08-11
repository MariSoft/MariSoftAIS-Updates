# Release Summary

This release introduces a complete workpack export workflow and several improvements to inspection data, task headers, dynamic tables, and video navigation.

## New Features

- Added **Export Workpack to New Database** wizard.
- Added identity-preserving data transfer so existing IDs remain unchanged.
- Added copying of required lookup and reference tables.
- Added support for exporting the currently selected:
  - Region
  - Site
  - Asset
  - Schedule
  - Workpack group
- Added selection of components and tasks to export.
- Added optional export of:
  - Anomalies
  - Events
  - Images
- Added copying of all related records at every required relationship level.
- Added copying of related `video_file` records used by task videos, images, and events.
- Added export review and final result pages.
- Added waiting indicators and detailed success/error reports.

## Workpack Export Fixes

- Ensured identity values are preserved for all exported records.
- Prevented SQL Server or XPO from automatically generating replacement IDs.
- Fixed reference-table copying when source and destination column counts differ.
- Fixed missing component and task dependencies in exported databases.
- Fixed missing related `Bound` and `Component` records.
- Fixed export failures caused by missing dynamic tables.
- Fixed creation and copying of component and task dynamic tables.
- Improved dependency ordering to maintain XPO relationships and referential integrity.

## Dynamic Table Improvements

- Dynamic table keys are now determined from the physical SQL table schema.
- Fixed dynamic tables being created without an XPO key.
- Fixed metadata initialization errors such as:
  - “Key property for type is absent.”
  - “Table has no physical column that can be used as its XPO key.”
- Fixed invalid primary-key/index creation for unsupported SQL column types.
- Ensured exported dynamic table definitions can be loaded correctly after connecting to the new database.

## Inspection Data Reload

- Implemented the inspection toolbar **Reload** command.
- Reload now runs the same process as the original **Load Data** command.
- Users can reload inspection data without returning to the database connection page.
- The current database connection and selected region, site, asset, schedule, and workpack are preserved.
- Existing traffic-light updates, waiting indicators, error handling, and duplicate-load protection are reused.

## Task Header Fixes

- Fixed an intermittent “Cannot access a disposed object” error after:
  - Starting a task.
  - Adding a new task header.
  - Setting the task end time.
- Task and header records are now reloaded by ID into the long-lived inspection XPO session before modification.
- Prevented newly created headers from remaining attached to temporary grid `session` instances.
- Preserved the selected header ID independently from temporary XPO objects.
- Users no longer need to refresh task headers before clicking **End Task**.

## Video Player Improvements

- Changed `mSeekForward2` to open the next `video_file` record.
- Changed `mSeekBackward2` to open the previous `video_file` record.
- Video records are ordered case-insensitively by `VideoFileName`, with `VF_ID` used as a tie-breaker.
- Records whose video files cannot be opened are skipped.
- The selected video record and task-clock reference are updated after navigation.
- Existing automatic next-video playback remains supported.

## General Improvements

- Improved XPO session and `session` lifetime handling.
- Improved synchronization between grids, selected records, and the video player.
- Added clearer diagnostic messages for export failures.
- Improved handling of partial or invalid exported databases.
- Verified the changes with successful builds containing no compilation warnings or errors.
