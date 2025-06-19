# 🛠️ Proceso de Manejo de Hotfix y Actualización de Ramas

Este documento describe el flujo estándar para aplicar un **hotfix** en una rama de producción y cómo propagarlo correctamente al resto de las ramas activas del repositorio.

---

## 📌 Supuestos

- La rama `main` (o `prod`) refleja el estado actual en producción.
- Se identificó un problema que requiere una corrección urgente (hotfix).
- La corrección debe integrarse posteriormente en ramas como `develop` y `release/*`.

---

## ✅ Pasos

### 1. Crear la rama de hotfix

```bash
git checkout main
git pull origin main
git checkout -b hotfix/fix-nombre-del-issue
```

Realiza aquí los cambios necesarios para corregir el problema.

---

### 2. Probar y desplegar el hotfix

- Realiza pruebas unitarias y funcionales.
- Valida el comportamiento en entorno QA/preproducción si aplica.
- Despliega a producción desde esta rama una vez validado.

---

### 3. Hacer merge del hotfix a `main`

```bash
git checkout main
git merge hotfix/fix-nombre-del-issue
git push origin main
```

---

### 4. Propagar el hotfix a `develop` (y otras ramas si aplica)

```bash
git checkout develop
git pull origin develop
git merge hotfix/fix-nombre-del-issue
git push origin develop
```

Repite con otras ramas (`release/x.y.z`, `feature/...`) si la corrección también aplica ahí.

---

## 🔁 Flujo visual

```
       main
        ▲
        │
 hotfix/fix-issue   ← rama temporal desde main
        │
        ▼
     producción ✅
        │
        ▼
     merge → main → 🔁 merge → develop (y otras ramas)
```

---

## 🧠 Recomendaciones

- Nombrar las ramas como `hotfix/login-error` o `hotfix/timeout-handler`.
- Usar `pull request` para todos los merges con reviewers asignados.
- Documentar si la corrección debe integrarse en otras ramas.
- Automatizar la validación en CI/CD si es posible.

---

**Autor:** Equipo DevOps / Arquitectura MuleSoft  
**Última actualización:** Junio 2025
