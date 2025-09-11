Jelly2Anki es un sistema que transforma tu servidor de Jellyfin en una herramienta de aprendizaje. Añade una interfaz de minería de frases directamente sobre el reproductor de video, permitiéndote crear tarjetas para Anki a partir de cualquier película o serie de tu colección.

El add-on funciona como el backend (el motor) del sistema, manejando el análisis de video, el corte de clips en formato **WebM** y la comunicación con Anki en segundo plano.

---
### **Guía de Inicio Rápido**

La instalación completa requiere 3 componentes.

**1. Requisitos Previos:**
*   **AnkiConnect:** [Instalar desde AnkiWeb](https://ankiweb.net/shared/info/2055492159).
*   **FFmpeg:** Debe estar instalado en tu sistema y accesible desde el PATH. [Descargar FFmpeg](https://ffmpeg.org/download.html).
*   **Tipo de Nota:** Un mazo con el tipo de nota necesario. `https://ankiweb.net/shared/info/1655427804?cb=1757575227535`

**2. Instalar el Backend (Este Add-on):**
1.  En Anki, ve a `Herramientas > Complementos > Obtener complementos...`
2.  Introduce el código: **`[código de AnkiWeb aquí]`**.
3.  Reinicia Anki.
4.  Ve a `Herramientas > Jellyfin Miner Backend Control` y haz clic en **`▶ Iniciar Servidores`**.

**3. Instalar la Extensión de Navegador:**
1.  **Descargar la Extensión:**
    *   Ve a la [**página de la última versión (Releases)**](https://github.com/co1000/jelly2anki/releases).
    *   En la sección "Assets" de la versión más reciente (arriba del todo), busca y descarga el archivo llamado `jelly2anki_Extension.zip`.
2.  **Instalar en el Navegador:**
    *   Descomprime el archivo `.zip` en una carpeta **permanente** en tu ordenador (por ejemplo, en `Mis Documentos/Jelly2Anki`).
    *   En Chrome/Brave/Edge, ve a la dirección: `chrome://extensions`.
    *   En la esquina superior derecha, activa el interruptor de **`Modo de desarrollador`**.
    *   Haz clic en el botón **`Cargar descomprimida`** y selecciona la carpeta **`extension`** que estaba dentro del ZIP que descomprimiste.

Una vez instalado, ve a un video en Jellyfin. Abre el panel lateral, haz clic en el engranaje (⚙️) y **configura las rutas a tus carpetas de medios**.

---
### **Soporte de Idiomas**

*   **Par de Idiomas Actual:** La versión Beta actual está optimizada para **hispanohablantes que aprenden inglés (ES -> EN)**. El análisis de vocabulario, el resaltado i+1 y las definiciones del diccionario están configurados para este par.

El soporte para más idiomas está considerado para futuras actualizaciones.

---
### **Características**

#### Interfaz de Minería Integrada
Jelly2Anki superpone una interfaz de usuario completa y no intrusiva directamente sobre el reproductor de video de Jellyfin.

*   **Panel Inferior:** Muestra el diálogo actual sincronizado con el video. Todas las palabras son interactivas, permitiendo abrir un diccionario con un solo clic.
*   **Panel Lateral:**
    *   **Pestaña de Subtítulos:** Una lista completa de todos los diálogos del video, que permite navegar rápidamente a cualquier punto de la conversación.
    *   **Pestaña de Palabras:** Un desglose de todo el vocabulario del video, clasificado por su estado de conocimiento (difícil, en aprendizaje, conocido).
*   **Atajos de Teclado:** Toda la interfaz responde a atajos de teclado para una minería más rápida y eficiente. La lista completa de atajos está disponible en la ventana de configuración de la extensión.

#### Asistente Inteligente de Subtítulos
El sistema elimina la necesidad de gestionar archivos de subtítulos manualmente. Al reproducir un video por primera vez, el asistente sigue una lógica automática:
1.  **Busca un archivo `.srt` externo:** Si encuentra un subtítulo en la misma carpeta que el video, lo utiliza inmediatamente.
2.  **Analiza pistas incrustadas:** Si no hay un archivo externo, inspecciona el video en busca de pistas de subtítulos internas.
    *   **Si encuentra una sola pista compatible,** la extrae, la guarda como un nuevo archivo `.srt` en la carpeta del video y la carga, todo de forma automática.
    *   **Si encuentra múltiples pistas,** presenta un menú flotante para que el usuario elija cuál desea utilizar. La selección se guardará como un nuevo archivo `.srt`.

#### Análisis de Vocabulario y Resaltado i+1
El núcleo de Jelly2Anki es su sistema para resaltar solo el vocabulario que es relevante para tu aprendizaje. En lugar de marcar todas las palabras "raras", utiliza un sistema de dos colores para darte información precisa:

*   <span style="color: #fda200;">**Naranja (Palabra Sugerida):**</span> Una palabra se marca en naranja si está por encima de tu nivel de vocabulario y el sistema no tiene constancia de que la conozcas. Es una sugerencia del sistema que dice: "Probablemente no conozcas esta palabra, podría ser un buen candidato para minar".

*   <span style="color: #45a1ff;">**Azul (Palabra en Aprendizaje):**</span> Una vez que minas una palabra (creando una tarjeta Anki con ella), se vuelve azul. Este color te ayuda a reconocer el vocabulario que estás estudiando activamente cada vez que aparece en un nuevo contexto.

Este sistema se alimenta de varias fuentes de datos para una máxima precisión:
*   Listas de frecuencia de palabras (CEFR A1-C2).
*   Tu nivel de vocabulario establecido en la configuración.
*   **Integración con AnkiMorphs:** Al iniciar el backend, el sistema lee tu base de datos de AnkiMorphs para tener un punto de partida preciso, evitando sugerir en naranja palabras que ya has aprendido en Anki.
*   Una base de datos local para las palabras que marcas manualmente como "conocidas" o "difíciles".

> **Futura Actualización:** Se está trabajando en una función de **sincronización dinámica**. En una futura versión, el sistema podrá releer periódicamente tu progreso en Anki. Esto permitirá que las palabras que estaban en azul (en aprendizaje) dejen de resaltarse automáticamente una vez que las hayas dominado en Anki, manteniendo el sistema siempre actualizado con tu conocimiento real.

#### Diccionario Emergente e Integración Externa
Hacer clic en **cualquier palabra** (resaltada o no) en el panel inferior abre un diccionario emergente multifuncional:

*   **Pestañas Internas:** Proporciona definiciones, datos fonéticos y ejemplos de uso de Reverso Context sin necesidad de salir del reproductor.
*   **Enlaces Externos:** Incluye botones de acceso directo para abrir la palabra consultada en diccionarios en línea populares (como Cambridge, WordReference y Merriam-Webster) en una nueva ventana emergente (popup).
*   **Control de Vocabulario:** Permite marcar manualmente el estado de la palabra (conocida/difícil), actualizando el resaltado en la interfaz en tiempo real.

#### Creación de Tarjetas con Clips WebM
El sistema está optimizado para crear tarjetas de alta calidad para Anki de forma eficiente.
*   **Procesamiento en Cola:** Al crear una tarjeta, la tarea se envía a un procesador en segundo plano. Puedes seguir viendo el video o minando otras frases sin esperar.
*   **Minado de Línea Única (`R`):** Crea una tarjeta para el diálogo actual.
*   **Minado por Fusión (`X` + `R`):** Permite seleccionar múltiples diálogos consecutivos y combinarlos en una sola tarjeta, ideal para conversaciones o contexto extendido.
*   **Formato `.webm`:** Todos los clips de video se generan en formato `.webm`, que ofrece un buen equilibrio entre calidad y tamaño de archivo, optimizado para Anki.
---
### **Notas Importantes**

 * Jelly2Anki se encuentra en fase **Beta** y está en desarrollo activo. Si encuentras algún problema, por favor, repórtalo en **[GitHub](https://github.com/co1000/jelly2anki/issues)**.
* La traducción automática de subtítulos actualmente se realiza con **Google Translate**, por lo que la calidad puede ser limitada.
* Este sistema está diseñado para funcionar con la **interfaz web por defecto** de Jellyfin. No se garantiza la compatibilidad con skins de terceros o temas de CSS personalizados, ya que pueden alterar la estructura de la página que la extensión necesita para funcionar.
* Al reproducir un video sin un archivo .srt externo, el sistema extraerá automáticamente una pista integrada; la calidad de este subtítulo depende del archivo original. Si prefieres usar otro, simplemente **reemplaza el archivo .srt generado** en la carpeta del video por uno de tu elección.
---
### **Demostraciones**

<img src="https://archive.org/download/chrome_D06hgBtAWq/chrome_D06hgBtAWq.gif" alt="Proceso de descarga, instalación y creación de tarjetas en Anki" width="60%">

**Reproductor de video de Jellyfin**
<img src="https://raw.githubusercontent.com/rebec0/static-assets/main/interfaz_inicial.jpg" alt="Interfaz Principal de Jelly2Anki en Jellyfin" width="100%">
<img src="https://github.com/rebec0/static-assets/releases/download/v1.0.0-assets/chrome_MhCT9xUopU.gif" alt="Interfaz Principal de Jelly2Anki" width="100%">
