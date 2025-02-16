# GlusterFS - Pruebas y Solución de Errores

## PRUEBAS

Para verificar el estado de los nodos y la correcta configuración de GlusterFS, ejecuta los siguientes comandos:

### 1. Verificar el estado del cluster
```bash
vagrant ssh gluster1
sudo gluster peer status
sudo gluster volume info
```

### 2. Verificar la correcta conexión del cliente
```bash
vagrant ssh client
df -h | grep glusterfs
```

### 3. Prueba de almacenamiento distribuido
```bash
vagrant ssh client
echo "Prueba de almacenamiento distribuido" | sudo tee /mnt/glusterfs/testfile.txt
```

### 4. Verificar la creación del archivo en los servidores GlusterFS
```bash
vagrant ssh gluster1
ls /gluster-storage/

vagrant ssh gluster2
ls /gluster-storage/
```

---

## CORREGIR ERRORES EJECUCIÓN ANSIBLE

Si experimentas problemas al ejecutar Ansible debido a errores de autenticación SSH, sigue estos pasos:

### 1. Eliminar la clave SSH antigua de cada máquina
Ejecuta los siguientes comandos para eliminar claves SSH incorrectas:

```bash
ssh-keygen -f "/home/pandakid/.ssh/known_hosts" -R "192.168.57.101"
ssh-keygen -f "/home/pandakid/.ssh/known_hosts" -R "192.168.57.102"
ssh-keygen -f "/home/pandakid/.ssh/known_hosts" -R "192.168.57.103"
```

### 2. Conectarte a cada máquina para aceptar la nueva clave SSH
Ejecuta los siguientes comandos e ingresa **yes** cuando se te solicite confirmar la conexión:

```bash
ssh vagrant@192.168.57.101 -i .vagrant/machines/gluster1/virtualbox/private_key
ssh vagrant@192.168.57.102 -i .vagrant/machines/gluster2/virtualbox/private_key
ssh vagrant@192.168.57.103 -i .vagrant/machines/client/virtualbox/private_key
```

### 3. Reintentar la ejecución de Ansible
Después de aceptar las nuevas claves SSH, intenta ejecutar nuevamente el playbook de Ansible con:

```bash
ansible-playbook -i inventory playbook.yml
```

