# Manual de GIT
---
## Borrar todo el historial de commits

Si lo que quieres es borrar todo el historial de commits y dejar la rama main vacía (como si el repositorio fuera nuevo) pero manteniendo tus archivos actuales, sigue estos pasos en la terminal:

1. Crear una rama temporal "huérfana" Esta rama no tendrá historial.
2. Añadir todos tus archivos actuales
3. Hacer el primer commit. Este será el "único" commit en tu nuevo historial.
4. Borrar la rama principal antigua y renombrar la nueva
5. Forzar la subida a GitHub
Cuidado: Esto sobrescribirá todo lo que hay en GitHub. Al ser una estructura de historial distinta, necesitas usar el comando "fuerza" (-f):
¿Por qué hacer esto?
Esto es útil si el historial se ha vuelto muy pesado, tiene errores de merge imposibles de arreglar o si quieres limpiar datos sensibles que subiste por error en el pasado.


```bash
git checkout --orphan temp_branch
git add -A
git commit -m "Initial commit (historial reseteado)"
git branch -D main
git branch -m main
git push -f origin main

```

---
## Des-registrar o eliminar la configuración de un usuario de Git

Para "des-registrar" o eliminar la configuración de un usuario de Git en tu máquina local, el proceso consiste en eliminar el nombre y correo electrónico asociados globalmente o en un repositorio específico.Aquí tienes los pasos detallados:

1. Eliminar la configuración global (Usuario predeterminado)Si configuraste un usuario para todos los repositorios de tu máquina, utiliza estos comandos en la terminal:
```bash
git config --global --unset user.name
git config --global --unset user.email
```
Esto elimina el usuario del archivo ~/.gitconfig.

2. Eliminar la configuración local (Solo para el repositorio actual)Si configuraste un usuario específico dentro de una carpeta de proyecto, dirígete a esa carpeta y usa:
```bash
git config --local --unset user.name
git config --local --unset user.email
```

3. Borrar credenciales guardadas (Windows/Mac)Git suele recordar contraseñas en el gestor de credenciales. Para evitar que Git siga usando el usuario anterior al hacer push/pull, debes borrar las credenciales almacenadas:
```
Windows: 
Busca "Administrador de credenciales" (Credential Manager) en el panel de control, busca las entradas de git:https://github.com y elimínalas.
```
```
macOS: Busca en "Acceso a Llaveros" (Keychain Access) y elimina las credenciales de github.com.
```
4. Verificar que se ha eliminadoPara confirmar que ya no hay usuario configurado, ejecuta:
```bash
git config --list
```
Si aparece user.name o user.email, repite los pasos anteriores.Nota: Esto no elimina tu cuenta de GitHub, solo desvincula al usuario de tu computadora local