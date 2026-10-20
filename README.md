# Centro de Servicios — Versión pública

Repositorio independiente para compilar y entregar el portal público. No contiene el panel administrador.

## Flujo de trabajo

### 1. Editar el portal administrador

1. Abre [el repositorio administrador](https://github.com/fercayvi/CENTRO-DE-SERVICIOS-VERSION-BASE-1.0).
2. Entra a **Code → Codespaces** y abre el Codespace de la rama `main`.
3. Ejecuta y prueba el portal administrador como de costumbre.
4. Edita los trámites, guarda los cambios y revisa que estén guardados en el workspace.
5. Haz commit y push de los cambios a `main`.

### 2. Sincronizar y generar el portal público

El flujo de GitHub Actions de este repositorio obtiene automáticamente desde `main` del repositorio administrador:

- `src/data.ts`
- Los archivos de `public/` (incluidas las imágenes y otros recursos locales).

Después instala las dependencias, valida TypeScript, compila la versión pública y genera un ZIP. La sincronización programada se ejecuta cada 15 minutos.

Para no esperar a la siguiente ejecución programada:

1. Abre la pestaña **Actions** de este repositorio.
2. Selecciona **Sincronizar y generar versión pública**.
3. Pulsa **Run workflow**, selecciona la rama `main` y vuelve a pulsar **Run workflow**.
4. Abre la ejecución que acaba de iniciar y espera a que termine en verde.

No es necesario copiar `data.ts`, copiar imágenes ni generar el HTML manualmente.

### 3. Descargar el ZIP final

1. Entra a la ejecución exitosa dentro de **Actions**.
2. Baja hasta **Artifacts**.
3. Descarga **portal-publico-zip**.
4. Descomprime el ZIP para verificar que `index.html` y la carpeta `assets/` estén incluidos.

El artefacto también incluye la carpeta compilada completa como **portal-publico**. Los artefactos de Actions se conservan durante 30 días, por lo que descarga el ZIP y guárdalo donde corresponda.

## Si falla la ejecución

Abre la ejecución fallida en **Actions**, entra al paso marcado en rojo y comparte el mensaje de error. El ZIP solo se genera cuando la validación y la compilación terminan correctamente.

## Vista previa en Codespaces (opcional)

Para probar el código de este repositorio manualmente:

```bash
npm ci
npm run lint
npm run build:public
npm run preview:public -- --host 0.0.0.0
```

Abre el puerto que Codespaces marque como disponible. La compilación pública queda en `dist-public/`; no edites esa carpeta a mano porque se vuelve a generar en cada compilación.
