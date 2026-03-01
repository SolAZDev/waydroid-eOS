# waydroid-eOS
eOS for Waydroid

Current version is [v3.5-t](https://gitlab.e.foundation/e/os/android/-/tree/v3.5-t) (based on Lineage 20) 
This following the [Instrctuions from the Waydroid Documentation]([red](https://docs.waydro.id/development/compile-waydroid-lineage-os-based-images#how-to-build))

To use, follow [these instructions](https://docs.waydro.id/faq/using-custom-waydroid-images)

### Special thanks to

- SuperChicken666 for their guidance
- Ronzz98 for their [build guide](https://community.e.foundation/t/ultimate-how-to-guide-unofficial-builds-using-repo-style-for-using-lineage-or-other-aosp-sources-that-are-not-supported-by-e-os/63908)

### Steps for Rebuilding
```bash
# Replace v3.5-t for your relevant version
repo init -u https://gitlab.e.foundation/e/os/android.git -b v3.5-t --git-lfs
repo sync build/make
wget -O - https://raw.githubusercontent.com/waydroid/android_vendor_waydroid/lineage-20/manifest_scripts/generate-manifest.sh | bash

# Remove or Comment out the <remove-project name="LineageOS/android_packages_apps_SetupWizard" /> line from .repo/local_manifests/01-removes.xml

repo sync --force-sync -j8 #Or -j$(nproc --all) -- This take a while, I  did it overnight, or while I was away.

. build/envsetup.sh # Do this in bash, if you aren't already.

apply-waydroid-patches
# Feel free to ignore the Vendor-add-more-build-types conflict.

lunch # and select which build you want.

# Finally Build.
make systemimage -j$(nproc --all) # Took me 2hrs
make vendorimage -j$(nproc --all) # Took me 1hr
```
