# PascalTZ

PascalTZ stands for "Pascal Time Zone". It allows you to convert between local times in various [time zones](http://en.wikipedia.org/wiki/Time_zone) and [GMT](http://en.wikipedia.org/wiki/Gmt)/[UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time), taking into account historical changes to time zone rules.

PascalTZ uses the [Time Zone Database](https://www.iana.org/time-zones) (often called `tz` or `zoneinfo`) to determine how to correctly adjust time for various time zones. The correctness of time zone conversions in future relies on using an up to date database. Beware, time zone rules may be changed by governments around the world, sometimes with a very short notice.

This code is based on PascalTZ originally published by *José Mejuto* in 2009.

The maintenance of this package has been taken up by *Denis Kozlov* in 2015 with key goals:

1. Identify and fix all data parsing and time zone conversion problems (yes, plenty).
2. Refactor the existing code to make debugging and maintenance easier.
3. Expand functionality for more user-friendly workflows.
4. Add test cases and a test framework.

See [USAGE.md](USAGE.md) for general usage instructions and known issues.

See [CHANGELOG.md](CHANGELOG.md) for a list of major changes between versions.

### Authors

- 2009 - José Mejuto
- 2015 - Denis Kozlov

### License

[Modified](COPYING.modifiedLGPL.txt)
[LGPL](COPYING.LGPL.txt) (same as the [FPC RTL](http://wiki.freepascal.org/FPC_modified_LGPL) and the Lazarus LCL).

### See Also

- [PascalTZ article on FPC Wiki](http://wiki.freepascal.org/PascalTZ)
- [PascalTZ repository in Lazarus CCR on SourceForge](http://sourceforge.net/projects/lazarus-ccr/files/PascalTZ/)
- [List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
