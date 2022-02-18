# Clone VMware VM from a Snapshot

Use the default cmdlets to clone the VM from a snapshot by creating a linked clone from the snapshot, then a full clone of the linked clone, then remove the linked clone.

```
$snap = Get-Snapshot -VM myVM -Name mySnapshot
New-VM -Name "$($snap.VM.Name)-linkedClone" -VMHost $snap.VM.VMHost -VM $snap.VM -ReferenceSnapshot $snap -LinkedClone
New-VM -Name "$($snap.VM.Name)-Clone" -VMHost $snap.VM.VMHost -VM "$($snap.VM.Name)-linkedClone"
Remove-VM -VM "$($snap.VM.Name)-linkedClone" -DeletePermanently -Confirm:$false
```
