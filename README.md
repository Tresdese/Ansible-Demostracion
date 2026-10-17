# Ansible: automatización y despliegue

Actividad de Desarrollo de Sistemas en Red. Práctica: configurar Nginx y publicar una página mediante un playbook. La presentación está diseñada para 24 minutos, incluida una demo de 5 minutos. El laboratorio del grupo toma 25–35 minutos después de preparar la VM.

## Entregables
- `Presentacion_Ansible.pptx`: presentación editable con notas para exponer.
- `Guia_Laboratorio_Ansible.pdf`: guía paso a paso, evidencias y reto.
- `Vagrantfile`, `inventory.ini`, `group_vars/`, `templates/`, `playbook.yml`: código ejecutable.
- `GUION_EXPOSICION.md`: tiempos, explicación y conducción de la demostración.
- `FUENTES.md`: documentación oficial consultada.

## Requisitos
- PC x86_64 con virtualización activada, Vagrant y VirtualBox compatibles instalados.
- Recomendado: 8 GB RAM en el anfitrión, 2 CPU disponibles y 10 GB de disco libre. La VM usa 1536 MB.
- Internet para descargar Ubuntu 22.04, Ansible y Nginx. Puerto 8080 libre.
- En Windows, ejecutar Vagrant en PowerShell del anfitrión; los comandos Linux se ejecutan dentro de `vagrant ssh`.
- No se necesita Ansible instalado en el anfitrión. La primera descarga se prepara ANTES de la clase.
- La carpeta compartida debe estar montada en `/vagrant`.

## Ejecución
1. Extraer el ZIP. Abrir una terminal dentro de la carpeta que contiene `Vagrantfile`.
2. En el anfitrión:
```bash
vagrant --version
VBoxManage --version
vagrant up --provider=virtualbox
vagrant ssh
```
3. Dentro de la VM:
```bash
cd /vagrant
ansible --version
ansible-inventory -i inventory.ini --graph
ansible web -i inventory.ini -m ansible.builtin.ping
```
4. Comprobar el estado inicial:
```bash
dpkg-query -W nginx
curl -I http://127.0.0.1
```
En una VM nueva se espera que Nginx no esté instalado y que la conexión HTTP falle. Estos fallos iniciales son parte de la evidencia; no continuar si existe un servidor que se necesite conservar.
5. Validar y desplegar:
```bash
ansible-playbook -i inventory.ini playbook.yml --syntax-check
ansible-playbook -i inventory.ini playbook.yml
curl -I http://127.0.0.1
systemctl is-active nginx
systemctl is-enabled nginx
```
6. En el navegador del anfitrión, abrir `http://127.0.0.1:8080`.
7. Repetir inmediatamente, sin editar archivos:
```bash
ansible-playbook -i inventory.ini playbook.yml
```
Se espera `changed=0`, `failed=0`, `unreachable=0`. Pasada una hora, la actualización de caché APT puede registrar un cambio; no confundirlo con un redespliegue.
8. Demostración de actualización: abrir `group_vars/web.yml` con un editor en el anfitrión y cambiar `app_version` de `"1.0"` a `"2.0"`. Ejecutar otra vez el playbook y recargar el navegador. No editar `/var/www/ansible-demo/index.html` manualmente.
9. Completar el reto de la guía. No se incluye su solución.

## Arquitectura del ejercicio
Vagrant crea la VM; el provisionador shell instala solamente Ansible y curl. Ansible instala y configura Nginx. En este laboratorio, el nodo de control y el nodo gestionado son la misma VM (`ansible_connection=local`). Por tanto, el ejercicio NO demuestra gestión remota por SSH. En un despliegue real, un controlador separado ejecutaría el mismo flujo sobre servidores del inventario mediante SSH.

El playbook sustituye `/etc/nginx/nginx.conf`: usarlo únicamente en la VM desechable del laboratorio, no sobre un servidor existente. La publicación de puerto se limita al equipo anfitrión. `become: true` utiliza sudo del usuario Vagrant.

## Comprobaciones adicionales
Después del primer despliegue:
```bash
ansible-playbook -i inventory.ini playbook.yml --check --diff
sudo nginx -t
```
El modo check predice cambios, pero no sustituye una ejecución real. No se recomienda usarlo como primera ejecución: recursos que aún no existen pueden causar errores en tareas posteriores. El módulo `ping` comprueba ejecución de Ansible, no envía ICMP.

## Detener y limpiar
Dentro de la VM: `exit`. En el anfitrión: `vagrant halt`. Para eliminar únicamente esta VM al terminar: `vagrant destroy` y confirmar la eliminación. Los archivos del proyecto permanecen.

## Publicación opcional en GitHub
Crear un repositorio vacío y ejecutar en la carpeta del proyecto:
```bash
git init
git add .
git commit -m "Agrega laboratorio de Ansible con Nginx"
git branch -M main
```
Después, configurar `git remote add origin URL_DEL_REPOSITORIO` con la URL real y ejecutar `git push -u origin main`. No subir llaves, contraseñas ni `.vagrant/`. No se ha creado ni publicado un repositorio automáticamente.

## Alcance de la validación
Ver `VALIDACION.md`. Las capturas de funcionamiento deben obtenerse al ejecutar el laboratorio: no se incluyen evidencias simuladas. Las versiones que resuelve APT y la box no están congeladas; registrar `ansible --version`, `nginx -v` y `vagrant box list` durante el ensayo.
