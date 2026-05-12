# Guía paso a paso: GitHub → Zenodo
## Para el artículo: *An Interpretable LLM-Based Classifier for Research Articles on MTSK*
### Revista: *Applied Artificial Intelligence* (Taylor & Francis)

---

## PARTE 1 — Subir el repositorio a GitHub

### Paso 1 — Crear una cuenta en GitHub (si no tienes)

1. Ve a https://github.com
2. Haz clic en **Sign up**
3. Completa el registro con tu correo institucional
4. Verifica tu correo

---

### Paso 2 — Crear el repositorio en GitHub

1. Inicia sesión en https://github.com
2. Haz clic en el botón verde **New** (esquina superior izquierda)
3. Completa el formulario:

   | Campo | Valor |
   |-------|-------|
   | Repository name | `mtsk-classifier` |
   | Description | `Interpretable LLM-based classifier for MTSK research articles — Applied Artificial Intelligence (Taylor & Francis)` |
   | Visibility | **Public** ← obligatorio para que la revista y los revisores puedan acceder |
   | Add a README file | Desmarcar (ya incluimos uno) |
   | Add .gitignore | Desmarcar (ya incluimos uno) |
   | Choose a license | Desmarcar (ya incluimos MIT License) |

4. Haz clic en **Create repository**
5. Copia la URL que aparece, por ejemplo:  
   `https://github.com/crojasc2/mtsk-classifier`

---

### Paso 3 — Preparar el repositorio localmente

Abre una terminal (o usa Google Colab con `!`) y ejecuta:

```bash
# Clonar el repositorio vacío que acabas de crear
git clone https://github.com/TU_USUARIO/mtsk-classifier
cd mtsk-classifier

# Copiar los archivos del proyecto a esta carpeta:
# - README.md
# - LICENSE
# - .gitignore
# - requirements.txt
# - notebooks/Experimento_13_SEED7.ipynb
# - docs/data_availability.md
```

> ⚠️ **IMPORTANTE antes de subir el notebook:**  
> Abre el notebook y verifica que no contiene:  
> - Tu token de Hugging Face (`hf_xxx...`) — ya está en `userdata.get()`, está bien  
> - Rutas absolutas con información personal sensible  
> - El archivo `.xlsx` del dataset (no debe subirse por derechos de autor)

---

### Paso 4 — Hacer el primer commit y push

```bash
cd mtsk-classifier

# Inicializar git y configurar identidad
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"

# Agregar todos los archivos
git add .

# Verificar qué se va a subir (no deben aparecer .xlsx ni .pt)
git status

# Crear el commit inicial
git commit -m "Initial commit: MTSK classifier — Experiment 13 SEED=7

Fine-tuned multilingual-e5-large for thematic classification of
MTSK research articles. Includes full training pipeline and SHAP
interpretability analysis.

Article: An Interpretable LLM-Based Classifier for Research
Articles on Mathematics Teaching Specialized Knowledge (MTSK)
Journal: Applied Artificial Intelligence (Taylor & Francis)"

# Subir al repositorio remoto
git push origin main
```

> Si git pide autenticación, usa tu usuario de GitHub y como contraseña  
> un **Personal Access Token** (no tu contraseña de GitHub):  
> GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → New token  
> Marca el permiso **repo** y genera el token.

---

### Paso 5 — Crear el Release v1.0.0

Este paso es necesario antes de conectar con Zenodo.

1. En tu repositorio en GitHub, haz clic en **Releases** (panel derecho)
2. Haz clic en **Create a new release**
3. Completa:

   | Campo | Valor |
   |-------|-------|
   | Tag version | `v1.0.0` |
   | Release title | `v1.0.0 — Initial release (Applied Artificial Intelligence)` |
   | Description | Pega el siguiente texto: |

   ```
   First release of the MTSK classifier code associated with the article:
   
   "An Interpretable LLM-Based Classifier for Research Articles on
   Mathematics Teaching Specialized Knowledge (MTSK)"
   
   Applied Artificial Intelligence — Taylor & Francis, 2025
   
   Includes:
   - Full fine-tuning pipeline (Experiment 13, SEED=7)
   - SHAP interpretability analysis
   - Confusion matrix and training curves
   - Data availability statement
   ```

4. Haz clic en **Publish release**

✅ Tu repositorio en GitHub está listo.

---

---

## PARTE 2 — Archivar en Zenodo (para obtener el DOI)

### Paso 6 — Crear cuenta en Zenodo

1. Ve a https://zenodo.org
2. Haz clic en **Sign up**
3. Puedes registrarte directamente **con tu cuenta de GitHub** (recomendado — facilita la integración automática)
4. Acepta los términos

---

### Paso 7 — Conectar Zenodo con GitHub

1. En Zenodo, haz clic en tu nombre de usuario (esquina superior derecha)
2. Selecciona **GitHub**
3. Haz clic en **Connect** junto a tu cuenta de GitHub
4. Autoriza el acceso cuando GitHub lo solicite
5. Verás la lista de tus repositorios públicos

---

### Paso 8 — Activar el repositorio mtsk-classifier en Zenodo

1. En la lista de repositorios, busca `mtsk-classifier`
2. Activa el toggle → debe quedar en **ON** (verde)

Zenodo ahora monitoreará automáticamente este repositorio.

---

### Paso 9 — Generar el DOI a partir del Release

Como ya creaste el Release `v1.0.0` en el Paso 5:

1. Ve a https://zenodo.org → tu perfil → **GitHub**
2. Busca `mtsk-classifier`
3. Haz clic en el release `v1.0.0` que aparece listado
4. Zenodo habrá creado automáticamente un registro

Si el release no aparece automáticamente:
1. En Zenodo, ve a **Upload** → **New upload**
2. Descarga el `.zip` del release desde GitHub  
   (en la página del release, botón **Source code (zip)**)
3. Arrastra el `.zip` al área de upload de Zenodo

---

### Paso 10 — Completar los metadatos en Zenodo

En la ficha de tu depósito en Zenodo, completa:

| Campo | Valor |
|-------|-------|
| **Upload type** | Software |
| **Title** | An Interpretable LLM-Based Classifier for Research Articles on Mathematics Teaching Specialized Knowledge (MTSK) |
| **Authors** | Rojas Celis, Carolina; Elorreaga, Luis Miguel |
| **Description** | Copia el abstract del artículo o un resumen técnico |
| **License** | MIT |
| **Keywords** | MTSK, text classification, LLM, mathematics education, SHAP, multilingual-e5-large, NLP |
| **Journal title** | Applied Artificial Intelligence |
| **Journal ISSN** | 0883-9514 |
| **Related identifiers** | URL de tu repositorio GitHub → tipo: *is supplemented by* |

Haz clic en **Save** y luego en **Publish**.

---

### Paso 11 — Copiar el DOI de Zenodo

Una vez publicado, Zenodo asignará un DOI con este formato:

```
https://doi.org/10.5281/zenodo.XXXXXXX
```

Cópialo. Este es el identificador que vas a usar en:

1. El manuscrito del artículo (en el **Data Availability Statement**)
2. El `README.md` de GitHub (reemplaza `[ZENODO_DOI]`)
3. El archivo `docs/data_availability.md`

---

### Paso 12 — Actualizar el README con el DOI y hacer push final

```bash
# Edita README.md: reemplaza [ZENODO_DOI] con el DOI real de Zenodo
# Edita docs/data_availability.md: reemplaza [ZENODO_DOI]

git add README.md docs/data_availability.md
git commit -m "Add Zenodo DOI: 10.5281/zenodo.XXXXXXX"
git push origin main
```

---

---

## RESUMEN FINAL

```
GitHub  →  https://github.com/TU_USUARIO/mtsk-classifier
Zenodo  →  https://doi.org/10.5281/zenodo.XXXXXXX
HuggingFace → https://huggingface.co/crojasc2/mtsk-classifier
```

### En el manuscrito, incluye ANTES de Referencias:

> The code and experimental notebooks used in this study are openly available
> on GitHub (https://github.com/TU_USUARIO/mtsk-classifier) and archived
> on Zenodo (https://doi.org/10.5281/zenodo.XXXXXXX). The fine-tuned
> classification model is available on Hugging Face at
> https://huggingface.co/crojasc2/mtsk-classifier. The annotated dataset
> is available upon reasonable request to the corresponding author.

---

## Checklist antes de enviar el artículo

- [ ] Repositorio GitHub público con notebook limpio (sin tokens ni datos)
- [ ] Release `v1.0.0` creado en GitHub
- [ ] Repositorio activado en Zenodo
- [ ] Metadatos completos en Zenodo (autores, journal, keywords)
- [ ] DOI de Zenodo obtenido y actualizado en README y manuscrito
- [ ] Modelo subido a Hugging Face Hub
- [ ] Data Availability Statement incluido en el manuscrito (antes de Referencias)
- [ ] DOI de Zenodo citado en la lista de referencias del artículo
