# 🔄 Actualización a v1.0.1 - Instrucciones

## 📌 Resumen de Cambios

Se ha realizado una **corrección crítica** en el servidor MCP-MAIL. La versión anterior (v1.0.0) estaba utilizando una API obsoleta del MCP SDK que impedía el correcto funcionamiento del servidor.

### 🐛 Problema Corregido

- **API Obsoleta**: El código usaba `McpServer` y el método `.tool()` que ya no existen en el SDK v1.22.0
- **Resultado**: Las herramientas no se registraban correctamente y Claude no podía ejecutarlas

### ✅ Solución Implementada

- Migración a la API correcta del SDK (`Server`, `ListToolsRequestSchema`, `CallToolRequestSchema`)
- Mejoras en el manejo de errores
- Validación robusta de variables de entorno
- Respuestas JSON más detalladas
- Mejor logging para debugging

## 🚀 Cómo Actualizar

### Opción 1: Pull desde Git (Recomendado)

Si tienes el repositorio clonado localmente:

```bash
# Navega al directorio del proyecto
cd /ruta/a/MCP-MAIL

# Obtén los últimos cambios
git pull origin main

# Reinstala las dependencias (por si acaso)
cd mcp-mail
npm install
```

### Opción 2: Descargar Release

1. Ve a [Releases](https://github.com/Joludime/MCP-MAIL/releases)
2. Descarga la versión v1.0.1
3. Extrae los archivos
4. Copia `mcp-mail/mcp-mail.mjs` a tu instalación actual

### Opción 3: Reemplazar Archivo Directamente

Descarga el nuevo `mcp-mail.mjs` desde:
```
https://raw.githubusercontent.com/Joludime/MCP-MAIL/main/mcp-mail/mcp-mail.mjs
```

## ⚙️ Después de Actualizar

### 1. Reiniciar Claude Desktop

**IMPORTANTE**: Debes reiniciar completamente Claude Desktop para que cargue el nuevo código.

- **macOS**: ⌘+Q para salir completamente, luego abre de nuevo
- **Windows**: Cierra desde la bandeja del sistema, luego abre de nuevo

### 2. Verificar la Configuración

Asegúrate de que tu `~/.claude_desktop_config.json` (o `%APPDATA%/Claude/claude_desktop_config.json` en Windows) esté configurado correctamente:

```json
{
  "mcpServers": {
    "mail-mcp": {
      "command": "node",
      "args": ["/ruta/completa/a/MCP-MAIL/mcp-mail/mcp-mail.mjs"],
      "env": {
        "Cuenta1-Morujo": "tu_correo@gmail.com",
        "PASSWORD_KEY": "tu_contraseña_app",
        "Cuenta2-Diaz": "segundo_correo@gmail.com",
        "Cuenta3-LoolBeh": "tercer_correo@gmail.com"
      }
    }
  }
}
```

### 3. Probar el Funcionamiento

Una vez reiniciado Claude Desktop, prueba con un comando simple:

```
Envía un correo de prueba desde la cuenta 1 a tu_correo@gmail.com 
con el asunto "Prueba MCP v1.0.1" 
y el mensaje "¡El servidor MCP-MAIL está funcionando correctamente!"
```

## 🔍 Verificar que Funciona

### Logs del Servidor

Si quieres ver los logs del servidor (útil para debugging):

```bash
cd /ruta/a/MCP-MAIL/mcp-mail
node mcp-mail.mjs
```

Deberías ver:

```
Servidor MCP-MAIL iniciado correctamente
Cuentas configuradas:
  - enviar_correo_cuenta1: tu_correo@gmail.com
  - enviar_correo_cuenta2: segundo_correo@gmail.com
  - enviar_correo_cuenta3: tercer_correo@gmail.com
```

### Respuesta de Claude

Después de enviar un correo, Claude debería responder con algo como:

```json
{
  "ok": true,
  "mensaje": "Correo enviado correctamente",
  "detalles": {
    "de": "tu_correo@gmail.com",
    "para": "destinatario@gmail.com",
    "asunto": "Prueba MCP v1.0.1",
    "messageId": "<...@gmail.com>",
    "respuesta": "250 2.0.0 OK ..."
  }
}
```

## 🐛 Solución de Problemas

### Error: "Herramienta no encontrada"

**Causa**: Claude Desktop no ha cargado el nuevo servidor

**Solución**:
1. Cierra completamente Claude Desktop
2. Verifica que la ruta en `claude_desktop_config.json` sea correcta
3. Abre Claude Desktop de nuevo

### Error: "PASSWORD_KEY no está configurada"

**Causa**: Las variables de entorno no están correctamente definidas

**Solución**:
1. Verifica que `PASSWORD_KEY` esté en tu configuración JSON
2. Asegúrate de usar una contraseña de aplicación de Gmail (no tu contraseña normal)
3. Reinicia Claude Desktop

### Error: "Email no configurado para X"

**Causa**: Una de las cuentas no tiene su email configurado

**Solución**:
1. Verifica que las variables `Cuenta1-Morujo`, `Cuenta2-Diaz`, etc. estén configuradas
2. Asegúrate de que los nombres coincidan exactamente (con guiones y mayúsculas)

### Las herramientas no aparecen en Claude

**Solución**:
1. Verifica la sintaxis JSON de tu configuración (sin comas extra, llaves bien cerradas)
2. Comprueba los logs de Claude:
   - **macOS**: `~/Library/Logs/Claude/`
   - **Windows**: `%APPDATA%/Claude/logs/`
3. Ejecuta el servidor manualmente para ver errores: `node mcp-mail.mjs`

## 📊 Cambios Técnicos Detallados

### Antes (v1.0.0) - ❌ No Funcionaba

```javascript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";

const server = new McpServer({...});
server.tool(nombreHerramienta, {...}); // ❌ Este método no existe
```

### Ahora (v1.0.1) - ✅ Funciona

```javascript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { 
  ListToolsRequestSchema, 
  CallToolRequestSchema 
} from "@modelcontextprotocol/sdk/types.js";

const server = new Server({...}, { capabilities: { tools: {} } });

// Registrar herramientas correctamente
server.setRequestHandler(ListToolsRequestSchema, async () => {...});
server.setRequestHandler(CallToolRequestSchema, async (request) => {...});
```

## 🆘 Necesitas Ayuda

Si después de seguir estas instrucciones sigues teniendo problemas:

1. **Revisa los logs**: Ejecuta el servidor manualmente para ver errores específicos
2. **Abre un Issue**: [GitHub Issues](https://github.com/Joludime/MCP-MAIL/issues/new/choose)
3. **Incluye**:
   - Sistema operativo
   - Versión de Node.js (`node --version`)
   - Contenido de logs (sin incluir contraseñas)
   - Pasos que seguiste

## 🎉 ¡Listo!

Una vez actualizado, tu servidor MCP-MAIL debería funcionar perfectamente. Ahora Claude podrá enviar correos desde tus cuentas configuradas sin problemas.

---

**Versión**: v1.0.1  
**Fecha**: 2025-11-17  
**Autor**: José Luis Díaz Mendoza
