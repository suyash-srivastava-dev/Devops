# SSH

## Generate SSH Key

refer: https://cloud.google.com/compute/docs/connect/create-ssh-keys
```
ssh-keygen -t rsa -f ~/.ssh/KEY_FILENAME -C USERNAME -b 2048
```

## Add Public Key to the VM
refer: https://devstudioonline.com/article/create-pem-private-key-and-connect-google-cloud-instance-form-terminal

For Static IP

- Open Google Console -> VPC Network -> External IP Address -> Change type to static and provide a name to this IP Address.

- Compute Engine -> VM Instances -> Click on name of your instance -> Edit

- In Remote Access Check Enable connection to serial ports.

- In SSH Keys section click on Show and edit. -> Click on Add Item

You will get the form to fill "Enter entire key data". Now open your gcserver.pub file and copy all content from this file and paste in SSH Keys form.

Now click on the Save button in the bottom and go back by Back arrow button on the top left corner. Now stop and start the Instance.

## Connect to VM

refer: https://cloud.google.com/compute/docs/connect/standard-ssh#openssh-client

```
chmod 400 PATH_TO_PRIVATE_KEY
ssh -i PATH_TO_PRIVATE_KEY USERNAME@EXTERNAL_IP
```