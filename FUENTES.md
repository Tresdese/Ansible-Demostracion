# Fuentes oficiales
Consultadas el 15 de octubre de 2026. El código del laboratorio es un ejemplo didáctico original.

1. Ansible, conceptos: https://docs.ansible.com/projects/ansible/latest/getting_started/basic_concepts.html
2. Ansible, playbooks e idempotencia: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_intro.html
3. Ansible, inventarios: https://docs.ansible.com/projects/ansible/latest/inventory_guide/intro_inventory.html
4. Ansible, handlers: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html
5. Ansible, módulo template y validación: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/template_module.html
6. Ansible, módulo apt: https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/apt_module.html
7. HashiCorp, provisionadores de Vagrant: https://developer.hashicorp.com/vagrant/docs/provisioning
8. HashiCorp, Ansible local: https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_local
9. HashiCorp, instalación de Vagrant: https://developer.hashicorp.com/vagrant/tutorials/get-started/install

La integración CI/CD y la comparación entre herramientas son una síntesis de su función; el paquete no configura un pipeline ni recursos de nube. La práctica usa shell para preparar Ansible y ejecución manual del playbook, no el provisionador ansible_local de Vagrant.
