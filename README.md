# Key generation

Generate signify key for signing repository metadata:

    signify -G -n -p apps.0.pub -s apps.0.sec

The `0` refers to the generation of the key. This is used for key rotation.

If you have your own OS where you can include an fs-verity key in the supported
keys built into the OS, you can also generate an fs-verity signing key in order
to provide continuous verification via verified boot instead of only having the
APK signatures verified at boot (which is actually largely skipped for most
boots for apps without fs-verity due to the performance cost).

Optionally, generate fs-verity signing key with `GrapheneOS` changed to an
arbitrary name representing your project (not used for anything):

    openssl req -newkey rsa:4096 -sha512 -noenc -keyout fsverify_private_key.0.pem -x509 -out fsverity_cert.0.pem -days 10000 -subj /CN=GrapheneOS/
    openssl x509 -in fsverity_cert.0.pem -out fsverity_cert.0.der -outform der

The `0` refers to the generation of the key. This is used for key rotation.

# Source definition

Available sources are defined in the sources of the Apps app.

1. class `PackageSource` defined in 

`app/src/main/java/app/grapheneos/apps/core/Repo.kt`

2. translated as `pkg_source_` in:

`app/src/main/res/values/strings.xml`
