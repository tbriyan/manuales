# Instalación y Configuración de Wayland en Kubuntu

Wayland maneja el escalado de pantallas de forma más eficiente que X11 en KDE Plasma. Sigue estos pasos para instalar y configurarlo en Kubuntu.

---

## 1️⃣ Verificar si Wayland está instalado
Ejecuta en la terminal:
```bash
echo $XDG_SESSION_TYPE
```
- Si responde `wayland`, ya lo estás usando.
- Si responde `x11`, aún estás en X11.

También puedes revisar si en la pantalla de inicio de sesión aparece la opción **Plasma (Wayland)**.

---

## 2️⃣ Instalar Wayland en Kubuntu
Si no está instalado, usa:
```bash
sudo apt update && sudo apt install plasma-workspace-wayland
```
Esto instalará los paquetes necesarios para usar Wayland con KDE Plasma.

---

## 3️⃣ Reiniciar e Iniciar Sesión en Wayland
1. Cierra sesión en Kubuntu.
2. En la pantalla de inicio de sesión, selecciona **Plasma (Wayland)**.
3. Inicia sesión.

---

## 4️⃣ Ajustar Escalado en Wayland
Ve a **Configuración del Sistema → Pantallas** y ajusta el escalado para cada monitor. Aplica los cambios y verifica que se conserven tras reiniciar.

---

## 5️⃣ Verificar que Wayland está corriendo
Ejecuta nuevamente:
```bash
echo $XDG_SESSION_TYPE
```
Debe devolver `wayland`.

---

## 6️⃣ Solución de Problemas
Si no puedes iniciar sesión en Wayland, instala paquetes adicionales:
```bash
sudo apt install plasma-workspace-wayland kwin-wayland-backend-drm
```
Luego reinicia e intenta iniciar sesión en **Plasma (Wayland)** nuevamente.

Si algunas aplicaciones no funcionan bien en Wayland, puedes ejecutarlas en X11 temporalmente:
```bash
QT_QPA_PLATFORM=xcb nombre-del-programa
```
Ejemplo:
```bash
QT_QPA_PLATFORM=xcb firefox
```

---

# Mejorando la Compatibilidad con Wayland

Si encuentras problemas con algunas aplicaciones, aquí hay soluciones alternativas.

## 1️⃣ Ejecutar Aplicaciones en X11 Dentro de Wayland
Para aplicaciones problemáticas, usa:
```bash
QT_QPA_PLATFORM=xcb nombre-del-programa
```
Ejemplo:
```bash
QT_QPA_PLATFORM=xcb firefox
```

## 2️⃣ Configurar Qt para Ejecutarse en XWayland
Si muchas aplicaciones Qt tienen problemas, edita `~/.profile` y agrega:
```bash
export QT_QPA_PLATFORM=xcb
```
Luego, reinicia sesión para aplicar los cambios.

## 3️⃣ Compartir Pantalla en Wayland con PipeWire
Si Zoom, Discord o Google Meet no funcionan, instala PipeWire:
```bash
sudo apt install pipewire wireplumber xdg-desktop-portal xdg-desktop-portal-kde
```
Luego reinicia el sistema.

## 4️⃣ Optimizar Soporte de Aplicaciones
- **Firefox y Chrome**: Habilita `MOZ_ENABLE_WAYLAND=1` para mejor rendimiento en Wayland.
- **Apps Electron (VS Code, Slack, Discord, etc.)**: Usa:
  ```bash
  --enable-features=UseOzonePlatform --ozone-platform=wayland
  ```

## 5️⃣ Volver a X11 si Wayland No Funciona Bien
Si experimentas demasiados problemas, puedes volver a X11:
1. Cierra sesión.
2. En la pantalla de inicio de sesión, selecciona **Plasma (X11)**.
3. Inicia sesión.

Para hacer X11 el predeterminado, ejecuta:
```bash
sudo update-alternatives --config x-session-manager
```
Y selecciona la opción de **Plasma (X11)**.

---

## 📌 Resumen
✅ Instalamos Wayland en Kubuntu.  
✅ Cambiamos la sesión de KDE a Plasma (Wayland).  
✅ Configuramos el escalado de forma nativa.  
✅ Solucionamos problemas de compatibilidad.  
✅ PipeWire ayuda a compartir pantalla.  
✅ Se puede volver a X11 si es necesario.  

Wayland mejora el escalado en pantallas de alta resolución y múltiples monitores. ¡Pruébalo y ajusta según sea necesario! 🚀

