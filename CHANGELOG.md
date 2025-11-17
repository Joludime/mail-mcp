# Changelog

Todos los cambios notables de este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.1] - 2025-11-17

### 🐛 Corregido
- **[CRÍTICO]** Actualización del servidor MCP a la API correcta del SDK v1.22.0
  - Migrado de `McpServer` obsoleto a `Server` actual
  - Implementación correcta de `ListToolsRequestSchema` y `CallToolRequestSchema`
  - Corrección del método de registro de herramientas (ya no se usa `.tool()`)
  - Mejora en la estructura de respuestas con formato JSON detallado
- Validación mejorada de variables de entorno
- Mensajes de error más descriptivos
- Mejor logging en stderr para debugging

### 🔄 Cambiado
- Estructura de respuesta ahora incluye más detalles (messageId, response, etc.)
- Soporte mejorado para HTML en el cuerpo del mensaje
- Conversión automática de saltos de línea a `<br>` en HTML

### 📝 Documentación
- Se documenta la corrección crítica de la API
- Actualización de ejemplos de uso

## [1.0.0] - 2025-11-14

### ✨ Agregado
- Servidor MCP inicial para envío de correos
- Soporte para múltiples cuentas de Gmail (3 cuentas configurables)
- Integración con Claude Desktop via MCP
- Configuración mediante variables de entorno
- Soporte para SMTP con Nodemailer
- Documentación completa en README
- Ejemplos de configuración (.env.example)
- Templates de Issues (Bug Report y Feature Request)
- Guía de contribución (CONTRIBUTING.md)
- Licencia MIT

### 🔐 Seguridad
- Protección de credenciales mediante .gitignore
- Uso de contraseñas de aplicación de Gmail
- Variables de entorno para datos sensibles

### 📝 Documentación
- README con badges y estructura profesional
- Instrucciones detalladas de instalación
- Guía de configuración paso a paso
- Ejemplos de uso
- Solución de problemas comunes

## [Unreleased]

### 🚀 En Desarrollo
- [ ] Soporte para Outlook/Office365
- [ ] Tests automatizados
- [ ] Configuración dinámica de cuentas
- [ ] Logs detallados
- [ ] Modo verbose para debugging

### 💡 Ideas Futuras
- [ ] Soporte para Yahoo Mail
- [ ] Adjuntos en correos
- [ ] Templates de correo
- [ ] Rate limiting
- [ ] Queue de correos
- [ ] Webhooks para notificaciones
- [ ] Dashboard web para monitoreo

---

## Tipos de Cambios

- ✨ **Agregado** para nuevas funcionalidades
- 🔄 **Cambiado** para cambios en funcionalidades existentes
- ⚠️ **Deprecado** para funcionalidades que se eliminarán pronto
- ❌ **Eliminado** para funcionalidades eliminadas
- 🐛 **Corregido** para corrección de bugs
- 🔐 **Seguridad** en caso de vulnerabilidades
