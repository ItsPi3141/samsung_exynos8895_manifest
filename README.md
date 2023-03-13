
<h1 align="center">
  Galaxy S8/S8+/Note 8
</h1>
<h3 align="center">
  Building instructions
</h3>
<hr>
<br>

## 🚀 Getting Started
To get started with Android, you'll need to get familiar with [Git and Repo](https://source.android.com/source/using-repo.html).

1. Set up your environment
```bash
sudo apt-get install git-core
git clone https://github.com/akhilnarang/scripts
bash scripts/setup/android_build_env.sh
```
<br>

2. Set up Git
```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
<br>

## 📁 Downloading Required Files
3. Create a folder for LineageOS
```bash
mkdir los
cd los
```
<br>

4. Initialize a local repository with LineageOS
```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-19.0 --depth=1
```
<br>

5. Create a `local_manifests` directory and copy the required manifest files to that directory
```bash
mkdir .repo/local_manifests
wget -O .repo/local_manifests/exynos8895.xml 'https://raw.githubusercontent.com/ItsPi3141/samsung_exynos8895_manifest/lineage-19.0/exynos8895.xml'
```
<br>

6. Sync the repositories
```bash
repo sync -c -f --force-sync
```
> ℹ️ If you have limited bandwidth, use this instead
> ```bash
> repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
> ```
<br>

## 🩹 Apply Patches
7. Clone patches into ~/patches
```bash
cd ~/
git clone https://github.com/8890q/patches
```
<br>

8. Move apply.sh into the `los` directory
```bash
mv patches/apply.sh los/
```
<br>

9. Apply patches
```bash
cd los
bash apply.sh
```
<br>

## 📝 Modifying Device Tree
> ℹ️ If you are building LineageOS, you can skip this section

If you are building for a ROM other than LineageOS, you will need to modify LineageOS references in the device tree. The following files will need to be modified according to your ROM:
- device/samsung/dreamlte/AndroidProducts.mk
- device/samsung/dreamlte/lineage_dreamlte.mk

- device/samsung/dream2lte/AndroidProducts.mk
- device/samsung/dream2lte/lineage_dream2lte.mk

- device/samsung/greatlte/AndroidProducts.mk
- device/samsung/greatlte/lineage_greatlte.mk
<br>

The following files will need to be renamed accordingly:
- device/samsung/dreamlte/lineage_dreamlte.mk
- device/samsung/dreamlte/lineage.dependencies

- device/samsung/dream2lte/lineage_dream2lte.mk
- device/samsung/dream2lte/lineage.dependencies

- device/samsung/greatlte/lineage_greatlte.mk
- device/samsung/greatlte/lineage.dependencies

- device/samsung/universal8895-common/lineage.dependencies
<br>

## 🛠️ Building ROM
10. Load device list
```bash
. build/envsetup.sh
```
<br>

11. Initiate build
```
breakfast <device_codename>
make bacon -j8
```
> ℹ️ Replace -j8 with the number of CPU threads you want to use. E.g. 20 threads: -j20. If build runs out of memory, try lowering the number of threads used

> ℹ️ Device codename can be the following:
> - dreamlte
> - dream2lte
> - greatlte

<hr>
<p align="center">
  Visit the <a href="https://wiki.lineageos.org">LineageOS Wiki</a> for more details on building.
</p>
