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
