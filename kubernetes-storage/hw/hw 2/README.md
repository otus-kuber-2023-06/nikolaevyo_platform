1. На вируталке с доп. диском создаём LVM раздел.
2. Настраиваем iSCSI по статье https://redos.red-soft.ru/base/server-configuring/other-utilites/iscsi/
   ЗЫ Для убунты это будет другой пакет sudo apt install targetcli-fb
3. На ноде кебера настраиваем инициализатор по той же статье раздел "Конфигурация клиента"
   На ноде нужно обязательно залогиниться 
   sudo iscsiadm -m node -T iqn.2003-01.org.linux-iscsi.cl16lgq25qclp9ao14e3-eluk.x8664:sn.8e01f2869c4d -p 10.129.0.12 -l
4. Применяем манифест поды. 
   targetPortal - Указываем адрес вируталки с доп. дисков
   iqn - указываем сгенерированный айди таргета
   В логах видим 
   AttachVolume.Attach succeeded for volume "iscsi-volume"    
5. Заходим в поду, записываем данные в примонтированный раздел
6. Делаем снапшот 
   sudo lvcreate -L 1G -s -n snap_vg0_iscsi /dev/mapper/VG0-iscsi
7. Удаляем данные, удаляем поду. Удаляем таргет
8. Восстанавливаем снапшот
   lvconvert --merge /dev/VG0/snap_vg0_iscsi
9. Делаем всё заново по статье https://redos.red-soft.ru/base/server-configuring/other-utilites/iscsi/
10. В манифесте поды заменяем айди таргета и деплоим. 
11. Заходим в поду и о чудо! Данные восстановились!