# Instalação (e recuperação) do GRUB no Arch Linux:

* Primeiro rodar ```lsblk``` e identificar a partição de /boot e a partição raiz (/)

* Após isso, roda:
```mount /dev/sda2 /mnt```
  **(onde geralmente fica a raiz, lembrando que o sdX (X pode ser a, b, c e etc. Exemplo -> sda ou sdb) se aplica a hdd/ssd sata).**

   **Para nvme,  é nvmeXn1 (esse X é a numeração do disco, exemplo -> nvme0n1)**
  
   **e por fim, vdX (onde o X pode ser a. b. c e etc. Exemplo -> vda entre outros)**

 * Rodar após:
 ``` mount /dev/sda1 /mnt/boot```
(geralmente é onde fica o /boot)

* Após a montagem, vamos rodar o comando ``` arch-chroot /mnt ```

* Dentro do chroot, rode:
``` pacman -Syu --noconfirm grub os-prober ```

* Após isso, vamos editar o arquivo conf do grub com o seguinte cmd:
``` sudo nano /etc/default/grub ```

* Após isso, procure dentro desse arquivo por ```#GRUB_DISABLE_OS_PROBER=false``` e retire o ```#``` antes do nome da variável para descomentar a mesma. 
* Após isso, segure control (ctrl) e clique na letra O e depois enter, após, segura control (ctrl) e clique em x para sair.

* Após isso, rode o comando caso seu S.O seja UEFI:
```grub-install --target=x86_64-efi --efi-directory=/boot  (check antes se o /boot/efi ou /boot/EFI existe, caso não, use o /boot) --bootloader-id=GRUB```

* Rode esse comando caso seu S.O seja em modo bios/legacy:
```grub-install /dev/sda (onde /dev/sda é seu disco)```

* Após tudo isso, rode o comando:
```grub-mkconfig -o /boot/grub/grub.cfg```
para gerar o arquivo de configuração do grub

* Após tudo isso der certo, apenas saia com exit e rode os comandos: 
```umount -R /mnt``` para desmontar todas partições montadas
e rode apenas ```reboot``` para reiniciar (ou ```reboot now``` para forçar)
