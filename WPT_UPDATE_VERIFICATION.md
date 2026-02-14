# WPT Test Data Update Verification

**Date**: 2026-02-14  
**WPT Repository Commit**: 75432af98fb4fa28308ac8301b35b1258c16ab33 (2026-02-14 15:10:59 +0100)

## Summary

This document records the verification that the Ada URL parser library's Web Platform Tests (WPT) test data is synchronized with the latest version from the upstream WPT repository at https://github.com/web-platform-tests/wpt.git.

## Actions Performed

1. **Executed URL test data update script**:
   ```bash
   ./tools/update-wpt.sh url
   ```
   - Successfully fetched latest test data from WPT repository
   - No changes detected - files already up to date

2. **Executed URLPattern test data update script**:
   ```bash
   ./tools/update-wpt.sh urlpattern
   ```
   - Successfully fetched latest test data from WPT repository
   - No changes detected - files already up to date

3. **Built and tested the library**:
   ```bash
   cmake -B build -DADA_TESTING=ON -G Ninja
   cmake --build build
   ctest --test-dir build --output-on-failure
   ```
   - Build completed successfully
   - All 188 tests passed (including 18 WPT-specific tests)
   - 0 failures

## Files Verified

All JSON test data files in `tests/wpt/` directory were verified to match the latest WPT repository:

### URL Test Data
- `urltestdata.json` ✓
- `urltestdata-javascript-only.json` ✓
- `setters_tests.json` ✓
- `IdnaTestV2.json` ✓
- `IdnaTestV2-removed.json` ✓
- `toascii.json` ✓
- `percent-encoding.json` ✓
- `verifydnslength_tests.json` ✓

### URLPattern Test Data
- `urlpatterntestdata.json` ✓
- `urlpattern-compare-test-data.json` ✓
- `urlpattern-generate-test-data.json` ✓

### Ada-specific Test Data
- `ada_extra_urltestdata.json` ✓
- `ada_extra_setters_tests.json` ✓
- `ada_long_urltestdata.json` ✓

## Conclusion

The Ada URL parser library's WPT test data is confirmed to be current and synchronized with the latest version of the Web Platform Tests repository. No updates were necessary at this time.

## Maintenance Notes

The repository includes automated scripts in `tools/update-wpt.sh` that make it easy to keep test data synchronized:

```bash
# Update URL test data
./tools/update-wpt.sh url

# Update URLPattern test data
./tools/update-wpt.sh urlpattern
```

These scripts use Git sparse-checkout to efficiently fetch only the necessary test resource files from the WPT repository.
