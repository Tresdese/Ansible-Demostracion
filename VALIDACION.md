# Validación del material

- Playbook: `ansible-playbook -i inventory.ini playbook.yml --syntax-check` terminó correctamente con ansible-core 2.17.14 en el entorno de preparación.
- Inventario: Ansible reconoció el grupo `web` y el host `web1`.
- Plantillas: ambas se renderizaron con las variables suministradas, sin variables Jinja2 pendientes.
- Presentación: 16 diapositivas, estructura PPTX comprobada y revisión visual.
- Guía: 7 páginas revisadas visualmente.

No hay Vagrant, VirtualBox ni systemd de una VM Ubuntu disponibles en el entorno de preparación. No se ejecutó el despliegue completo, no se midió la idempotencia real y no se obtuvieron capturas de Nginx funcionando. La validación de sintaxis no equivale a una prueba de integración.

El entorno de clase instala la versión de ansible-core disponible en APT de Ubuntu 22.04, que puede diferir de la usada para la revisión. Las tareas utilizan módulos builtin comunes; ensayar con la VM antes de presentar. El paquete no congela las versiones de la box o los paquetes.

Antes de entregar: completar integrantes, ejecutar la guía y añadir las capturas propias. Ante errores, consultar la sección de diagnóstico y conservar la salida real.
