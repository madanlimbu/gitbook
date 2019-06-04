# VirtualBox Sharing file

## Sharing File with Virtual Machine

In this post, we will learn to be able to share a folder and files inside it with a [virtual machine \(Virtual Box\)](https://www.virtualbox.org/).

1. Create new folder in your main computer and Virtual Machine _**\(“Share-Location”\)**_
2. Select bidirectional copy in Virtual Machine Menu
3. Choose the folder created in your main computer as Shared location in shared preference setting of Virtual Box and give a _**\(“Shared-Name”\)**_
4. Install vboxsf from Virtual Box menu \(also known as guest additions\)
5. Finally, mount host share folder with guest share folder using follow command in virtual machine: 

```text
sudo mount -t vboxsf ("Shared-Name" Give In Virtual Box Settings) ("Share-Location" In VM )
```

