## 🔍 Reporte de Auditoría QA

**Auditor:** Nicolas Martinez
**Repositorio auditado:** Cityfix8
**Fecha:** 2026-06-02

---

## ❌ Resultado de las pruebas

El contenedor levanta correctamente pero las pruebas fallan porque
Jest no está instalado dentro del contenedor.

## 🪲 Bug encontrado

El `Dockerfile` ejecuta `npm install` pero Jest no está listado como
dependencia en el `package.json`, o el `node_modules` no se está
copiando correctamente durante el build.

## 📋 Log de la terminal

cityfix-container  | > cityfixapp@1.0.0 test
cityfix-container  | > jest
cityfix-container  | sh: jest: not found

## 🛠️ Causa raíz

Jest no queda instalado dentro del contenedor al momento del build.
Puede deberse a que falta en `devDependencies` del `package.json`
o a un problema en el `Dockerfile` al copiar/instalar dependencias.

## ✅ Fix sugerido en el fork

Verificar que el `package.json` tenga Jest en `devDependencies`:

```json
"devDependencies": {
  "jest": "^29.0.0"
}
```

Y que el `Dockerfile` ejecute `npm install` antes de copiar el código,
o usar `npm install --include=dev` para incluir dependencias de desarrollo.