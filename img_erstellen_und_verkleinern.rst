Abbild erstellen
====================

.. code:: bash

  dd if=/dev/sdb of=~/Projekte/2013_RPi-SPS/raspbian_with_mongodb_2013_01_05.img


Loop-device einhängen
====================

.. code:: bash 

  modprobe -r loop

.. code:: bash

  modprobe loop max_part=5

Wenn loop in den Kernel kompiliert wurde, muss man

.. code::
  loop.max_part=5

an die Kernelparamter anhaengen.  Ein setzten ueber
/sys/module/loop/parameters/max_part scheint nicht moeglich.


Dauerhafte Konfiguration ueber */etc/modprobe.d*. (siehe *man modprobe.d*)


.. code:: bash

  losetup --show -f <Datei.img>


Image verkleinern
====================

.. code:: bash

  sudo gparted /dev/loop0

Sektorgröße ermitteln
~~~~~~~~~~~~~~~~~~~~

.. code:: bash

  fdisk -l ~/Projekte/2013_RPi-SPS/raspbian_with_mongodb_2013_01_05.img

.. TODO fdisk Beispiel ausgabe

.. code:: bash

  truncate -s $(((SECSIZE+1)*512)) ~/Projekte/2013_RPi-SPS/raspbian_with_mongodb_2013_01_05.img

.. code:: bash

  e2fsck /dev/loop0p2 


Nach dem kopieren auf die sd-Karte kann wieder *gparted* verwenden werden um
die Partition auf die maximal Größe auszudehnen.
