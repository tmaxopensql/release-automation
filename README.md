# Release Automation
This repository contains github action for release automation. The automation system follows the policies introduced below.

## OpenSQL Version Policy
### Semantic Versioning
- We follow [semantic versioning](https://semver.org/) with a slight customization
```
    □    .    ■    .    ◆
  Major     Minor     Patch
```
- Minor becomes 0 when Major version has changed
- Patch becomes 0 when Minor version has changed
- Version must change incrementally (ex. 1.0.1 -> 1.0.2 -> 1.0.3 -> 1.1.0)

### Major Version
- At first, the major version is set to be 0, indicating that the project is at pre-released initial stage
- After the project is thought to be ready for public production stage, the major version is set to be 1
- Products with the same major version must be compatible with each other
- Major version must change when: 
  - the project reached public production stage level
  - a newly added feature is not compatible with the current major version
  - a significant changes in architecture cause incompatibility

### Minor Version
- Minor version must change when:
  - critical errors like undefined behavior or abnormal crash have been fixed
  - a supplementary fixes have been added following a newly added features
  - a new feature that is compatible with the current minor version has been added
  - a performance enhancement has been added

### Patch Version
- Patch version must change when: 
  - a fix to non-critical bugs has been added
  - a fix to dependency versions has been added
  - a fix to README.md has been added
  - a fix to tests or test framework has been added
  - a simple refactoring has been added

## OpenSQL Branch Policy
- [Branch Policy](http://192.168.1.153:8080/index.php/%EC%82%AC%EC%9A%A9%EC%9E%90:%EC%9D%B4%EC%83%81%EB%AA%85/Policy/OpenSQL_versioning)
