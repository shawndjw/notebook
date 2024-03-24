# Installing Kobo-InkBox

I have an old Kobo N705 e-reader that I can't seem to update with material anymore so I will be replacing the original Kobo software with [Kobo-Inkbox](https://github.com/Kobo-InkBox/inkbox). This will allow me to continue using the Kobo as a reader as I love the small form factor and find it quite pleasing to read from.

## Steps

### Remove back cover

1. There are two back covers that need to be removed. The first is just decorative and snaps off. Looking at the unit from the back pry the back off from the top left corner, there's a small opening you can use with a fingernail or a flathead screwdriver.
2. The second cover is fastened using 6 small philips screws. You will require a small philips screwdriver to remove the screws. Then use a small flathead screwdriver to carefully pry the cover off.

### Install Kobo-Inkbox

I will be keeping the 4GB MicroSD intact as a backup and will be replacing it with an 8GB card.

1. Download the latest pre-compiled binaries from the link in the GitHub repository README (I'm currently using Inkbox 2.0).

2. Check to make sure that the file integrity is intact.

```bash
$ cat inkbox-2.0-n705.xz.sha256
2e103043cafe391b75d37907c25f5a5d1437f1e630008c612c882d19ff837446
$ sha256sum inkbox-2.0-n705.xz
2e103043cafe391b75d37907c25f5a5d1437f1e630008c612c882d19ff837446  inkbox-2.0-n705.xz
```

3. Flash 8GB MicroSD card. The shows up as /dev/sda for me but becareful as this is usually the root drive. It isn't in my case as my root is using an nvme drive and shows up as /dev/nvme0

```bash
$ xzcat inkbox-2.0-n705.xz | sudo dd of=/dev/sda
$ sync
```
4. Remove the 4GB MicroSD card by pulling out of the slot and replace it with the newly imaged MicroSD. Boot up the device and that's it. Enjoy!




