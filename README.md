# 🎓 Proyecto Colaborativo: Matriz de Perfiles Profesionales (FODA)

Este proyecto es una aplicación web basada en **Python (Flask)** y **Docker** que recopila dinámicamente los perfiles FODA de todos los ingenieros en formación de la clase.

El objetivo es simular un entorno de desarrollo real con **Integración Continua (CI)**, donde 24 desarrolladores contribuyen simultáneamente al mismo repositorio sin generar conflictos.

---

## 🏗 Arquitectura del Proyecto

El sistema está diseñado con una arquitectura de microservicio modular. 
**⚠️ IMPORTANTE:** Para evitar conflictos, solo debes trabajar en tu archivo personal dentro de la carpeta `students`.

```text
proyecto-foda/
├── .github/workflows/      # 🤖 CI: Aquí viven los YAMLs que validan tu código
├── app/
│   ├── static/             # Archivos CSS/JS globales (NO TOCAR)
│   ├── templates/
│   │   ├── base.html       # Layout maestro
│   │   ├── index.html      # Dashboard principal (NO TOCAR)
│   │   └── students/       # 🟢 TU ZONA DE TRABAJO
│   │       ├── template_foda.html  <-- Plantilla base
│   │       └── juan_perez.html     <-- Tu archivo final
│   └── main.py             # Lógica del Backend
├── Dockerfile              # Configuración de contenedor
└── requirements.txt        # Dependencias

```
Flujo de Trabajo (Workflow)
Tienes 1 hora para desplegar tu perfil. Sigue estos pasos estrictamente para pasar las validaciones automáticas (CI).
1. Preparación del Entorno
2. Haz un Fork de este repositorio a tu cuenta personal de GitHub.
Clona tu fork a tu máquina local:git clone [https://github.com/TU_USUARIO/nombre-repo.git](https://github.com/TU_USUARIO/nombre-repo.git)
cd nombre-repo
3. Creación de la Rama (Branch Policy)
El sistema de CI rechaza commits directos a main o ramas mal nombradas.
Crea una rama siguiendo el estándar: feature/nombre-apellido
# ✅ Correcto
git checkout -b feature/amawta-chacha

# Incorrecto (El CI fallará)
git checkout -b mi-tarea
git checkout -b update-foda

3. Desarrollo de tu Perfil
Navega a la carpeta de plantillas:cd app/templates/students/
Haz una copia del archivo template_foda.html con tu nombre (usando guiones bajos):Ejemplo: juan_perez.htmlEdita tu archivo HTML:
Llena los cuadrantes del FODA.NO uses estilos inline ```text (<div style="...">).``` Usa solo las clases CSS predefinidas (fortalezas, debilidades, etc.).
NO toques el archivo index.html ni base.html.

5. Prueba Local (Opcional pero recomendado)
Antes de subir, verifica que tu tarjeta aparece en el dashboard.
Con Python:Bash# En la raíz del proyecto
pip install -r requirements.txt
python app/main.py
# Visita http://localhost:5000
Con Docker:Bashdocker build -t foda-app .
docker run -p 5000:5000 foda-app

5. Envío a ProducciónSube tus cambios a tu repositorio (Fork):Bashgit add app/templates/students/tu_archivo.html
git commit -m "feat: add foda profile for [Tu Nombre]"
git push origin feature/nombre-apellido
Ve a GitHub y abre un Pull Request (PR) hacia la rama main del repositorio original.

Validaciones Automáticas (CI Pipelines)

Al abrir tu PR, se ejecutarán automáticamente los siguientes YAMLs de validación. Si alguno falla, tu código NO será integrado.
CheckDescripciónQué hacer si fallaBranch NamingVerifica que tu rama empiece con feature/Crea una rama nueva con el nombre correcto y
vuelve a subir.HTML SyntaxBusca etiquetas mal cerradas o errores de sintaxisRevisa tu HTML, asegúrate de cerrar todos los </div>.
Docker BuildVerifica que el proyecto compileSi solo tocaste tu HTML, esto no debería fallar.

Despliegue Continuo (CD)

El despliegue a producción es manejado centralizadamente.Una vez que tu PR tenga todos los checks en Verde (✅),
será revisado por el Lead (Profesor).Al ser aprobado (Merged), se disparará un pipeline oculto que despliega la nueva
versión en una instancia AWS EC2.Tu perfil aparecerá en vivo minutos después.📝 Resumen de Comandos RápidosBash# 1. Rama
git checkout -b feature/tu-nombre

# 2. Copiar template (Linux/Mac)
cp app/templates/students/template_foda.html app/templates/students/tu_nombre.html

# 3. Subir
git add .
git commit -m "feat: mi foda"
git push origin feature/tu-nombre
¡Buena suerte, Ingenieros!

