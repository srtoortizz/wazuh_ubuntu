
  # Instalación y Configuración de Wazuh para Monitorización de Seguridad

## Descripción del Proyecto

Este proyecto documenta la instalación y configuración de un servidor Wazuh en una máquina virtual para monitorizar eventos de seguridad de otra máquina con Windows Server 2022. El objetivo es detectar eventos de seguridad, como inicios de sesión mediante SSH desde otra máquina virtual (Kali Linux), y enviar alertas de seguridad por correo electrónico utilizando SMTP.

![Esquema_implementación drawio](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/676b57c7-4cf6-4383-b005-e59bfa9f9fdd)




## Prerrequisitos

- Una máquina virtual con una distribución Linux (para el servidor Wazuh) (Se ha empleado Ubuntu 16)
- Una máquina virtual con Windows Server 2022
- Una máquina virtual con Kali Linux
- Acceso a Internet para descargar paquetes y dependencias

## Pasos de Instalación

### 1. Instalación del Servidor Wazuh

1. **Actualiza los paquetes de tu sistema**:
    ```bash
    sudo apt-get update && sudo apt-get upgrade
    ```

2. **Instala Wazuh**:
    Sigue las [instrucciones oficiales de instalación de Wazuh] (https://documentation.wazuh.com/current/installation-guide/index.html) para tu distribución de Linux.

   ![Wazuh_install](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/45790545-7b09-4ed6-abdb-5b3d8b70fef0)

![wazuh_installsh](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/0ce3135b-f910-4e10-96c6-f540b6763685)

Al finalizar la instalación de Wazuh nos proporcionará las credenciales para poder acceder al dashboard

![credencialeswazuh](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/04acb33d-933d-49bb-afed-79c2d8412232)
![dashboard](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/5b4a6e3f-c4e5-43ba-86ae-24a9070a05b0)

Comprobamos que todo funcione correctamente
![check_wazuh_dashboard](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/526a6673-46c2-423f-bd43-6fb236604dfe)
![dashboard](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/e6257a2c-2be2-49fa-a980-1087ebfcd9e2)


### 2. Configuración del Agente Wazuh en Windows Server 2022

1. **Descarga el agente Wazuh para Windows**:
    Puedes descargar el agente desde la [página oficial de Wazuh](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html).

   ![manageagent](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/ae90f30c-2191-4c44-9a48-dc6a4dada42c)


3. **Instala el agente Wazuh en Windows Server 2022**:
    Sigue el asistente de instalación e introduce los datos del servidor Wazuh cuando se te solicite.
![agent_manager_wazuh_configuracion](https://github.com/srtoortizz/wazuh_ubuntu/assets/57291029/66b35051-f639-49b2-8c4a-a8786427f903)

   

5. **Configura el agente**:
    Edita el archivo `ossec.conf` en el directorio de instalación del agente para asegurarte de que está correctamente configurado para comunicarse con el servidor Wazuh. 

### 3. Monitorización de Eventos de Seguridad

1. **Configura la monitorización de eventos en Wazuh**:
    Asegúrate de que las reglas necesarias están habilitadas en el archivo de configuración de Wazuh para detectar eventos específicos como inicios de sesión SSH. Puedes encontrar más información sobre la configuración de reglas en la [documentación de reglas de Wazuh](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/index.html).

2. **Prueba de detección**:
    Realiza un inicio de sesión SSH desde Kali Linux a Windows Server 2022 para verificar que los eventos son correctamente capturados por Wazuh.

### 4. Configuración del Envío de Alertas por Correo Electrónico

1. **Configura el servidor SMTP en Wazuh**:
    Edita el archivo `ossec.conf` en el servidor Wazuh para añadir la configuración SMTP. Un ejemplo de configuración SMTP sería:
    ```xml
    <global>
      <email_notification>yes</email_notification>
      <smtp_server>smtp.tu_servidor.com</smtp_server>
      <email_from>tu_correo@dominio.com</email_from>
      <email_to>destinatario@dominio.com</email_to>
    </global>
    ```

2. **Prueba de envío de alertas**:
    Genera un evento de seguridad y verifica que se envía una alerta por correo electrónico. Para más detalles sobre la configuración de notificaciones por correo, revisa la [guía de notificaciones por correo de Wazuh](https://documentation.wazuh.com/current/user-manual/notifications/email-notification/index.html).

## Tecnologías Utilizadas

- Wazuh
- Windows Server 2022
- Kali Linux
- SMTP

## Conclusión

La implementación de Wazuh en este entorno permite una monitorización eficaz de los eventos de seguridad, proporcionando alertas en tiempo real y mejorando la capacidad de respuesta ante posibles amenazas.

## Referencias

- [Documentación Oficial de Wazuh](https://documentation.wazuh.com/current/index.html)
- [Guía de Instalación de Wazuh](https://documentation.wazuh.com/current/installation-guide/index.html)
- [Configuración del Agente Wazuh](https://documentation.wazuh.com/current/user-manual/agents/registering-agents/index.html)
- [Reglas de Wazuh](https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/index.html)
- [Notificaciones por Correo en Wazuh](https://documentation.wazuh.com/current/user-manual/notifications/email-notification/index.html)


s
