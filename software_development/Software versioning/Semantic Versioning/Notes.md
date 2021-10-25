Given a version number **MAJOR.MINOR.PATCH**, increment the:
  1. **MAJOR** version when you make incompatible API changes,
  2. **MINOR** version when you add functionality in a backwards compatible manner, and
  3. **PATCH** version when you make backwards compatible bug fixes.

Major version zero (0.y.z) is for initial development. Anything MAY change at any time. The public API SHOULD NOT be considered stable.
  - It is suggested to start at 0.1.0 and bump the minor version on every breaking change to the public API.
  - You can increment to 1.0.0 when you are in a position to appropriately control and manage these breaking changes.

Version 1.0.0 defines the public API. The way in which the version number is incremented after this release is dependent on this public API and how it changes.
