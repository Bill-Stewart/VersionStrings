# VersionStrings.pp

## Author

Bill Stewart (bstewart AT iname.com)

## License

**VersionStrings.pp** is covered by the GNU Lesser Public License (LPGL). See the file `LICENSE` for details.

## Description

**VersionStrings.pp** is a Free Pascal (FPC) unit for checking the validity of and comparing version numbers in string format.

## Reference

This section documents the functions in the unit.

A version number string uses the following format:

_a_[`.`_b_[`.`_c_[`.`_d_]]]

Where _a_, _b_, _c_, and _d_ are values from 0 to 65535, inclusive, separated by dots. Parts _b_, _c_, and _d_ are optional and are assumed to be 0 if not specified. The following are examples of valid version strings:

* **10** - same as **10.0.0.0**
* **10.3** - same as **10.3.0.0**
* **10.3.251** - same as **10.3.251.0**
* **10.4.2500.32124**

A string that does not conform to the above rules is not a valid version string. The following are examples of version strings that are not valid:

* **10.65536** - contains a part greater than 65535
* **-3** - negative values not allowed
* **10,3** - string contains characters other than numbers or dots

---

### TestVersionString

Tests whether a specified version string is valid. See above for a description of a valid version string.

#### Syntax

```
function TestVersionString(const VersionString: UnicodeString): Boolean;
```

#### Parameters

`VersionString` - Specifies the version string to test for validity.

#### Return Value

The function returns `true` if the version string is valid, or `false` otherwise.

---

### CompareVersionStrings

Compares two version strings.

#### Syntax

```
function CompareVersionStrings(const VersionString1, VersionString2: UnicodeString): Integer;
```

#### Parameters

`VersionString1` - Specifies a version string to compare.

`VersionString2` - Specifies a version string to compare.

#### Return Value

The return value will be less than 0 if `VersionString1` is less than `VersionString2`, 0 if `VersionString1` is equal to `VersionString2`, or greater than 0 if `VersionString1` is greater than `VersionString2`.

The return value will be 0 if either version string is not a valid version string, so it is recommended to validate both `VersionString1` and `VersionString2` before relying on the return value from this function.

#### Examples

See the following table for return value examples:

Expression                              | Return Value
--------------------------------------- | ------------
`CompareVersionStrings('10', '10.0')`   | 0
`CompareVersionStrings('1.10', '1.09')` | > 0
`CompareVersionStrings('2.3.0', '2.5')` | < 0
