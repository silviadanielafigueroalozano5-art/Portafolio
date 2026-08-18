# 📋 Directorio de Usuarios

Aplicación web interactiva que muestra un directorio de usuarios con información completa obtenida de la API RandomUser.

## 🎯 Características

- ✅ **Directorio de 102 usuarios** con fotos, nombres y datos básicos
- ⭐ **Sistema de favoritos** - Marca usuarios como favoritos y guárdalos en localStorage
- 🔄 **Caché inteligente** - Los usuarios se almacenan en localStorage para acceso rápido
- 📄 **Detalle completo** - Ve toda la información personal de cada usuario
- 🗺️ **Integración con Google Maps** - Visualiza ubicación y coordenadas
- 📱 **Diseño responsivo** - Funciona perfectamente en móviles y desktop
- 🔄 **Sincronización** - Los favoritos se sincronizan entre páginas

## 📁 Estructura del Proyecto

```text
tarjetas/
├── index.html      # Página principal - Directorio de usuarios
├── tarjeta.html    # Página de detalle - Información completa del usuario
├── style.css       # Estilos CSS para tarjeta.html
└── README.md       # Este archivo
```

## 🏗️ Arquitectura

### index.html - Directorio Principal

**Responsabilidades:**

- Obtiene usuarios de la API RandomUser.me (150 usuarios)
- Filtra duplicados por email y foto
- Cachea los usuarios en localStorage
- Muestra tarjetas en dos vistas: "Todos" y "Favoritos"
- Gestiona el sistema de favoritos

**Variables globales:**

- `usuarios[]` - Array de todos los usuarios cargados
- `tabActual` - Controla qué pestaña está activa ('todos' o 'favoritos')
- `TOTAL` - Número máximo de usuarios (102)
- `CLAVE_CACHE` - Clave localStorage para el caché ('usuarios_v5')

### tarjeta.html - Detalle del Usuario

**Responsabilidades:**

- Carga datos del usuario desde localStorage
- Muestra toda la información personal
- Permite marcar/desmarcar como favorito
- Genera links a Google Maps

**Datos mostrados:**

- Información personal: nombre, género, edad
- Contacto: email, teléfono
- Ubicación: dirección, ciudad, estado, país, código postal
- Datos de registro: usuario, fecha de registro, años registrado
- Ubicación geográfica: zona horaria, coordenadas, links a Google Maps

### style.css - Estilos Generales

- Estilos específicos para tarjeta.html
- Colores coherentes con paleta de diseño
- Diseño responsivo (max-width: 500px)
- Animaciones suaves y transiciones

## 🔄 Flujo de Datos

```text
┌─────────────────────────────┐
│   index.html (Directorio)   │
└──────────────┬──────────────┘
               │
          Click tarjeta
               │
               ▼
┌─────────────────────────────┐
│ localStorage.usuarioSeleccionado
│ localStorage.favoritos      │
└──────────────┬──────────────┘
               │
          Lee datos
               │
               ▼
┌─────────────────────────────┐
│   tarjeta.html (Detalle)    │
└─────────────────────────────┘
```

## 💾 LocalStorage

### Claves utilizadas

**`usuarios_v5`** - Array de todos los usuarios

```javascript
[
  {
    gender: "male",
    name: { title: "Mr", first: "John", last: "Doe" },
    location: { street, city, state, country, coordinates, timezone },
    email: "...",
    phone: "...",
    picture: { large: "..." },
    dob: { date: "...", age: 30 },
    registered: { date: "...", age: 5 },
    login: { username: "..." },
    nat: "US"
  },
  ...
]
```

**`favoritos`** - Array de usuarios marcados como favoritos

```javascript
[
  { /* usuario completo */ },
  ...
]
```

**`usuarioSeleccionado`** - Usuario actualmente visto en tarjeta.html

```javascript
{ /* usuario completo */ }
```

## 🛠️ Funciones Principales

### index.html

| Función                           | Descripción                                        |
| --------------------------------- | -------------------------------------------------- |
| `cargarUsuarios()`                | Carga desde caché o inicia fetchDesdeAPI()         |
| `fetchDesdeAPI()`                 | Obtiene usuarios de la API RandomUser              |
| `filtrarDuplicados(lista)`        | Elimina duplicados por email/foto                  |
| `recargarUsuarios()`              | Limpia caché y obtiene nuevos usuarios             |
| `toggleFavorito(indice, evento)`  | Agrega/quita usuario de favoritos                  |
| `mostrarTodos()`                  | Renderiza todas las tarjetas                       |
| `mostrarFavoritos()`              | Renderiza solo tarjetas favoritas                  |
| `cambiarTab(tab)`                 | Alterna entre "Todos" y "Favoritos"                |
| `verTarjeta(indice)`              | Abre la página de detalle                          |

### tarjeta.html

| Función                     | Descripción                           |
| --------------------------- | ------------------------------------- |
| `obtenerFavoritos()`        | Lee favoritos de localStorage         |
| `guardarFavoritos(lista)`   | Guarda favoritos en localStorage      |
| `esFavorito(email)`         | Verifica si es favorito               |
| `toggleFavoritoTarjeta()`   | Alterna favorito en la página detalle |
| `actualizarEstrella()`      | Actualiza visual de la estrella       |

## 🎨 Paleta de Colores

```css
--primary: #789eee          /* Azul principal */
--primary-dark: #2b3a55     /* Azul oscuro */
--bg: #f0f2f5               /* Fondo claro */
--card-bg: #ffffff          /* Fondo tarjetas */
--text: #333333             /* Texto principal */
--text-light: #666666       /* Texto secundario */
--star: #f5c518             /* Amarillo para estrella activa */
--star-empty: #ccc          /* Gris para estrella inactiva */
--male: #4a90d9             /* Azul para género masculino */
--female: #d94f8c           /* Rosa para género femenino */
```

## 📡 API RandomUser

**Endpoint:** `https://randomuser.me/api/`

**Parámetros:**

- `results=150` - Número de usuarios a obtener
- `seed=directorio100v1` - Semilla para resultados reproducibles

**Respuesta:** JSON con array de objetos usuario

## 🚀 Cómo Usar

1. **Abrir index.html** en un navegador
2. **Esperar a que carguen** los usuarios (primera vez)
3. **Hacer clic en una tarjeta** para ver detalles completos
4. **Hacer clic en la estrella** para marcar/desmarcar como favorito
5. **Cambiar de pestaña** para ver solo favoritos
6. **Obtener nuevos usuarios** con el botón de recarga

## ⚙️ Tecnologías

- **HTML5** - Estructura semántica
- **CSS3** - Estilos y animaciones
- **Vanilla JavaScript** - Sin dependencias
- **LocalStorage** - Almacenamiento local
- **Fetch API** - Consumo de API REST
- **Google Maps API** - Integración de mapas

## 🔗 Enlaces Externos

- [RandomUser API](https://randomuser.me/)
- [Google Maps](https://www.google.com/maps)

## 📝 Notas Técnicas

- Los usuarios se cachean para evitar llamadas repetidas a la API
- El sistema de favoritos usa email como identificador único
- La búsqueda de duplicados verifica tanto email como foto
- Los datos persisten en el navegador mediante localStorage
- Compatible con navegadores modernos (Chrome, Firefox, Safari, Edge)

---

**Última actualización:** 2026-08-18
