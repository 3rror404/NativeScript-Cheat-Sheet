# NativeScript-Cheat-Sheet
Often used. Rarely remembered.

---

## Update `tns-core-modules` and `tns-core-modules-widgets`

1. 
```
$ tns plugin remove tns-core-modules
$ tns platform remove android
$ tns platform remove ios
$ tns plugin add tns-core-modules
$ tns platform add android
$ tns platform add ios
```

2. Add signing identity to xcode project.
