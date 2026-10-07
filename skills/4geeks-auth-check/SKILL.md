---
name: 4geeks-auth-check
description: Verifica si la sesión de 4Geeks Academy está activa consultando el endpoint /v1/admissions/user/me.
---

# 4Geeks Auth Check

## Cuándo usar

Usa esta skill cuando el usuario quiera saber si su token de 4Geeks Academy sigue siendo válido y tiene una sesión activa.

## Secreto requerido

- `FOURGEEKS_TOKEN` — Token de autenticación para la API de BreatheCode/4Geeks.

## Endpoint

- **URL base:** `https://breathecode.herokuapp.com`
- **Ruta:** `GET /v1/admissions/user/me`
- **Autenticación:** `Authorization: Token <token>`

## Procedimiento

1. Obtén el token del secreto `FOURGEEKS_TOKEN` usando la herramienta `secrets` con `action=list` para verificar que existe, o intenta usarlo directamente. **No muestres, loguees ni hardcodees el valor del token.**

2. Realiza una petición HTTP GET a `https://breathecode.herokuapp.com/v1/admissions/user/me` con el header:
   ```
   Authorization: Token <valor_del_token>
   ```

   Usa la herramienta `exec` con `curl` para la petición. Pasa el token como variable de entorno para no exponerlo en los logs:
   ```sh
   curl -s -w "\n%{http_code}" -H "Authorization: Token ${FOURGEEKS_TOKEN}" https://breathecode.herokuapp.com/v1/admissions/user/me
   ```

3. Interpreta la respuesta según el código HTTP:

   | Código | Significado |
   |--------|-------------|
   | **200** | ✅ Sesión activa y token válido. Devuelve los datos del usuario. |
   | **401** | ❌ Token inválido o no proporcionado. |
   | **403** | ❌ Token válido pero sin permisos suficientes. |
   | Otro / error de red | ⚠️ Error inesperado o de conectividad. Informa del código y mensaje. |

4. Responde al usuario con un mensaje claro:
   - Si es 200: indica que la sesión está activa y muestra el email o nombre del usuario si viene en la respuesta.
   - Si es 401: indica que el token ha expirado o es inválido, sugiere regenerarlo.
   - Si es 403: indica que falta permisos, sugiere contactar soporte.
   - Si hay error de red: indica que no se pudo contactar el servidor.

## Output esperado

La skill no modifica archivos. Solo informa al usuario el resultado de la verificación.