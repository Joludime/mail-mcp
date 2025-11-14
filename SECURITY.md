# Política de Seguridad

## 🔒 Versiones Soportadas

Actualmente se proporcionan actualizaciones de seguridad para las siguientes versiones:

| Versión | Soportada          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |

## 🚨 Reportar una Vulnerabilidad

La seguridad de MCP-MAIL es una prioridad. Si descubres una vulnerabilidad de seguridad, por favor reportala de manera responsable.

### Cómo Reportar

**NO** abras un issue público para vulnerabilidades de seguridad.

En su lugar:

1. **Envía un email** a: joludime291076@gmail.com
2. **Incluye** en tu reporte:
   - Descripción detallada de la vulnerabilidad
   - Pasos para reproducir el problema
   - Impacto potencial
   - Versión afectada
   - Cualquier solución propuesta

### Qué Esperar

- **Confirmación**: Recibirás una respuesta en 48 horas
- **Evaluación**: Evaluaremos el reporte en 7 días
- **Actualización**: Te mantendremos informado del progreso
- **Resolución**: Trabajaremos en un parche lo antes posible
- **Crédito**: Te daremos crédito (si lo deseas) cuando se publique el fix

## 🛡️ Mejores Prácticas de Seguridad

### Para Usuarios

1. **Contraseñas de Aplicación**
   - SIEMPRE usa contraseñas de aplicación, no tu contraseña principal
   - Genera contraseñas únicas por aplicación

2. **Variables de Entorno**
   - NUNCA compartas tu archivo `.env`
   - NUNCA hagas commit de credenciales
   - Usa `.env.example` como template

3. **Actualizaciones**
   - Mantén Node.js actualizado
   - Actualiza las dependencias regularmente
   - Revisa el CHANGELOG antes de actualizar

4. **Permisos**
   - Limita acceso al archivo de configuración de Claude
   - No compartas tokens o credenciales
   - Revoca contraseñas de aplicación no utilizadas

### Para Desarrolladores

1. **Dependencias**
   - Ejecuta `npm audit` regularmente
   - Actualiza dependencias con vulnerabilidades conocidas
   - Usa versiones específicas en package.json

2. **Código**
   - No hardcodees credenciales
   - Valida todas las entradas
   - Usa HTTPS para todas las comunicaciones
   - Implementa rate limiting cuando sea apropiado

3. **Testing**
   - Prueba con credenciales de prueba
   - Nunca uses credenciales reales en tests
   - Implementa tests de seguridad

## 🔐 Vulnerabilidades Conocidas

Actualmente no hay vulnerabilidades conocidas. Esta sección se actualizará si se descubren problemas de seguridad.

## 📚 Recursos de Seguridad

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Node.js Security Best Practices](https://nodejs.org/en/docs/guides/security/)
- [Gmail App Passwords](https://support.google.com/accounts/answer/185833)

## 🙏 Agradecimientos

Agradecemos a todos los investigadores de seguridad que reportan vulnerabilidades de manera responsable.

---

**Última actualización**: Noviembre 2025
