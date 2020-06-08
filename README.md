# Utils

## Tools

### Benchmark

```shell
$ benchmark URL
0.12345 sec
```

### Check Accessibility

```shell
$ check_accessibility URL
CHECK ACCESSIBILITY
Validate Accessibility (BITV 1.0 - Level 2):
OK|FAIL
Validate Accessibility (Section 508):
OK|FAIL
Validate Accessibility (Stanca Act):
OK|FAIL
Validate Accessibility (WCAG 1.0 - Level AAA):
OK|FAIL
Validate Accessibility (WCAG 2.0 - Level AAA):
OK|FAIL
```

### Check Validation

```shell
$ check_validation URL
CHECK VALIDATION
Validate W3C:
OK|FAIL
Validate CSS 3:
OK|FAIL
Validate CSS 2.1:
OK|FAIL
Validate CSS 2:
OK|FAIL
Validate CSS Mobile:
OK|FAIL
Validate Feed:
OK|FAIL
Validate HTTP Headers:
OK|FAIL
Validate Semantics:
OK|FAIL
Validate Links:
OK|FAIL
```

## Notes

 - Freeze the requirements: `pip3 freeze > requirements.txt`
 - Install the requirements: `pip3 install -r requirements.txt`
