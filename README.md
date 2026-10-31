# Sistema de Gestión del Asilo de Ancianos «Cabeza de Algodón»

Proyecto final del curso **Análisis y Diseño de Sistemas II** — Universidad Mariano Gálvez de Guatemala, Centro Regional de Mazatenango.
Autor: **Gilmer Iván Ortiz Samayoa** (carné 3090-23-12685) · Catedrático: Ing. Angel Atilio Maltez C.

Aplicación web para la administración diaria del asilo: residentes y su expediente clínico (ficha, notas, signos vitales y medicación), citas médicas, laboratorio, inventario y farmacia, habitaciones, facturación y donaciones, reportes, usuarios con cuatro roles, bitácora y respaldo.

## Arquitectura

Cliente-servidor en tres capas:

| Capa | Tecnología | Archivos |
|---|---|---|
| Presentación | HTML5, CSS3, JavaScript | `Sistema/index.html`, `css/app.css`, `js/app.js` |
| Lógica de negocio | JavaScript + PHP 8 (PDO) | `js/servicios.js`, `js/auth.js`, `js/datos.js`, `api/api.php` |
| Datos | MySQL 8 / MariaDB 10.4+ | `Sistema/basedatos/*.sql` (18 tablas, 9 vistas, 3 procedimientos) |

Seguridad: contraseñas con PBKDF2-SHA256 (100 000 iteraciones, sal de 16 bytes), contraseñas iniciales temporales con cambio obligatorio, bloqueo de 30 s tras 3 intentos, permisos por rol revisados en el servidor y transacciones.

## Instalación (XAMPP)

1. Copiar la carpeta `Sistema` en `C:\xampp\htdocs\`.
2. En phpMyAdmin importar, en orden, `01_esquema.sql`, `02_datos.sql` y `03_consultas.sql` (para hosting usar `basedatos/hosting/`).
3. Revisar `Sistema/api/config.php`.
4. Abrir `http://localhost/Sistema/`. La contraseña temporal del administrador se entrega por separado; el sistema obliga a cambiarla.

Sin servidor, `Sistema/index.html` abre en **modo demostración** con datos ficticios guardados en el navegador.

## Documentación

- `Documentacion/Linea_base/` — ERS v3.0 (documento oficial), respuesta al informe SQA y planificación.
- `Documentacion/PDF/` — Arquitectura, fases de análisis, diseño y desarrollo, historias de usuario, manual de diseño visual, manual de usuario, metodología real y requerimientos.
- `Documentacion/Diagramas/` — modelo ER, casos de uso, secuencia, estados, actividades, clases y despliegue.

## Pruebas

`Evidencias/pruebas/` contiene 46 pruebas automatizadas con Python + Playwright (23 de verificación de hallazgos SQA y 23 funcionales). Resultado del 22/10/2026: **46 de 46 aprobadas**. Ver `Evidencias/pruebas/LEEME.txt`.

> Este repositorio no contiene contraseñas. Todos los datos de ejemplo son ficticios.
