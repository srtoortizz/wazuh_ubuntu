

  # Instalación y Configuración de Wazuh para Monitorización de Seguridad

## Descripción del Proyecto

Este proyecto documenta la instalación y configuración de un servidor Wazuh en una máquina virtual para monitorizar eventos de seguridad de otra máquina con Windows Server 2022. El objetivo es detectar eventos de seguridad, como inicios de sesión mediante SSH desde otra máquina virtual (Kali Linux), y enviar alertas de seguridad por correo electrónico utilizando SMTP.

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
    Sigue las [instrucciones oficiales de instalación de Wazuh](https://documentation.wazuh.com/current/installation-guide/open-distro/all-in-one-deployment.html) para tu distribución de Linux.

### 2. Configuración del Agente Wazuh en Windows Server 2022

1. **Descarga el agente Wazuh para Windows**:
    Puedes descargar el agente desde la [página oficial de Wazuh](https://documentation.wazuh.com/current/installation-guide/open-distro/win-agent/index.html).

2. **Instala el agente Wazuh en Windows Server 2022**:
    Sigue el asistente de instalación e introduce los datos del servidor Wazuh cuando se te solicite.

3. **Configura el agente**:
    Edita el archivo `ossec.conf` en el directorio de instalación del agente para asegurarte de que está correctamente configurado para comunicarse con el servidor Wazuh. Consulta la [documentación oficial de configuración del agente](https://documentation.wazuh.com/current/user-manual/agents/registering-agents/index.html) para más detalles.

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


