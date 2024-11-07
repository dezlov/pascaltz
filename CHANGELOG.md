# Change Log

This change log contains the highlights of major changes. For details on all finer changes please check the commits history.

## Latest development version

Enhancements:

* Compatibility changes for building the test runner project with FPC 3.2.0.

Bugfixes:

* Handle unabbreviated month names in Zone and Rule definitions. For example, "Mexico" rule definition in tzdata 2024b.

## 2.2.0 (2020-03-18)

Enhancements:

- Replaced `.rc` script by `.res` resource file in order to avoid issues with `windres` on some platforms.
- Added high-DPI component icons.

Bugfixes:

- Handle weekday macros which fall into another month. For example, "Asia/Hong_Kong" zone in tzdata 2019b includes weekday macros "Sun>=28" and "Sun>=31".

## 2.1.3 (2019-08-15)

Bugfixes:

- Extended allowed time specification from 24:00:00 to 25:00:00. The 25:00:00 time introduced in tzdata 2018f, see "Rule Japan 1948 1951".
- Handle negative static DST offset in Zone definition. For example, "Europe/Prague" zone definition in tzdata 2018g.

## 2.1.2 (2018-04-05)

Bugfixes:

- Fixed loading of time zone data directory via `DatabasePath` property on Unix-like platforms.

Miscellaneous:

- Added Online Package Manager (OPM) update JSON file.
- Added instructions for creating a new release.

## 2.1.1 (2018-02-21)

Miscellaneous:

- Updated package file version number.

## 2.1 (2018-02-19)

Features:

- Added auxiliary `LocalTime`, `UniversalTime`, `UnixTime` class functions.
- Published `DetectInvalidLocalTimes` property. Available at design time.
- Added `DatabasePath` published property. Allows specifying the database path (file or directory) at design time, which will be automatically loaded at runtime.
- Created a design and runtime package for Lazarus IDE.
- Converted `TPascalTZ` class to a component.

Enhancements:

- Strict time string parsing with allowed range 00:00:00 to 24:00:00, where each time components is also checked independently.

Bugfixes:

- Support longer time zone abbreviations in 2017b. Increased `TZ_TIMEZONELETTERS_SIZE` from 8 to 11.
- Avoid compiler range check errors for "24:00" time string notation.

Miscellaneous:

- Added randomly generated test vectors using PHP 7.2.0 and tzdata 2017.3.
- Moved randomly generated test vectors to individual subfolders.
- Randomly generated test vectors are no longer a part of the default test suite, because they cannot be tested consistently, because they are dependent on specific versions of tzdata.
- Use independently configured directories for tzdata and vectors in the test runner.
- Display configuration parameters and the list of loaded test vector files in the test runner.

## 2.0 (2016-07-19)

Features:

- Implemented a testing framework. It includes test vectors for regressions, randomly generated test vectors with PHP code and unit testing of internal functions.
- Added `UnixToLocalTime` and `LocalTimeToUnix` methods.
- Added `Convert` method for converting between two specific time zones.
- Added `ToString` methods for stringifying Zone and Rule objects.
- Ability to load standard files from "tzdata" package via `ParseDatabaseFromDirectory` method.
- Added `ParseDatabaseFromString` method.
- Added `ClearDatabase` method.
- Added `ParseDatabaseFromMemory` function.
- Removed unused return value from all `ParseDatabaseFromXXX` functions.
- Removed `AOnlyGeoZones` parameter from `GetTimeZoneNames` function, as it is inaccurate and infeasible.
- Removed public `ProcessedLines` property, in favor of `CountZones`, `CountRules`, `CountLinks` properties.
- Added `CountZones`, `CountRules`, `CountLinks`, `CountTimeZoneNames` properties.
- Implemented parsing and use of LINK zone tag for resolving zone aliases.
- Added `TimeZoneExists` function to check for existence of a zone.
- Added `ParseDatabaseFromFiles` function for loading multiple database files at once by combining them into a single stream.

Performance:

- Sort zone definitions by ZONE UNTIL date. Ensures correct operation of the zone selection algorithm when original input is not sorted.
- Recoded algorithm that searches for applicable rule. Select the most recently activated rule by comparing target date and rule begin date in UTC forms using previous save time offset. A more consistent and transparent implementation.
- Moved `LocalTimeToGMT` and `GMTToLocalTime` operating on `TTZDateTime` type to public section. This should allow to overcome alleged limitations of `TDateTime` type.
- Significant speedup of time zone conversions due to smart storage of zones and rules (grouped by their name).
- Removed rule sorting code. Sorting rules after parsing is no longer necessary.
- Eliminated dependency on custom sorting classes, replaced with built-in list sort functionality.
- Major code refactoring and cleanup.

Bugfixes:

- Handle special cases when rule begin date is same as zone begin date (a.k.a. previous zone end date), meaning that rule begin date in UTC should be calculated based on previous zone offset and save time.
- Use time form of ZONE UNTIL field when determining applicable zone definition.
- Removed limitation for allowing to parse only one database stream. It no longer silently corrupts internal data.
- Fixed incorrect interpretation of time string in shortest form, i.e. time in hours.
- Fixed inappropriately adjusted rule begin dates according to RULE AT field's time form (universal, standard, wall clock).
- Fixed a problem with incorrectly adjusted dates when correcting overlapping seconds of day. Calculation of Days Since AD (DSAD) was replaced with Julian Day Number (JDN).
- Fixed a problem of not applying rules inherited from prior years (prior to the year of the date in question), by finding the most recently activated rule out of all rules.
- Correctly interpret all official forms of time (wall clock, standard, universal) in ZONE and RULE definitions.
- Fixed incorrect resolution of negative seconds in `FixUpTime`.
- Fixed incorrect selection of appropriate DST rule, by ensuring that only the latest applicable rule is used.
- Fixed mishandling of parameters and wrong use of `MacroFirstWeekDay` and `MacroLastWeekDay` functions, resulting in wrong values for non first or last week days (e.g. 2nd or 3rd week day).
- Fixed incorrect parsing of conditional parts in `MacroSolver` function (e.g. "Sun>=15").
- Fixed double freeing of internal objects in ParseLine.
- Increased the maximum allowed length of zone name from 30 to 32 characters, to support 'backward' zones.
- Do not break official zone names at parsing stage by replacing '_' (underscore) with ' ' (space) in zone names.

## 1.0 (2009-11-10)

**Warning:** Major data parsing and time zone conversions problems are present in PascalTZ 1.0. You are strongly advised to use a newer version.

- Original version published by *José Mejuto*.
