# Configuración de Pantalla en Kubuntu

Si la resolución de tu laptop se ve muy pequeña y al conectar un monitor externo los elementos se ven demasiado grandes, puedes configurar la escala de la pantalla correctamente para que se conserve incluso después de reiniciar el sistema.

1️⃣ Ajustar Escalado en KDE Plasma

Abre Preferencias del sistema.

Ve a Pantalla y monitor → Escalado de pantalla.

Ajusta el porcentaje de escalado según sea necesario (por ejemplo, 125% o 150%).

Aplica los cambios y cierra sesión para que surta efecto.

Si esto no se aplica correctamente tras reiniciar, prueba con la configuración manual a través de la terminal.

2️⃣ Configurar Escalado con xrandr (X11)

Si estás en X11 y la interfaz gráfica no guarda la configuración:

xrandr --output eDP-1 --scale 1.25x1.25

Reemplaza eDP-1 con el identificador correcto de tu pantalla. Para verificarlo, usa:

xrandr | grep " connected"

Para hacer que este cambio se aplique al iniciar sesión, agrega el comando a ~/.xprofile o ~/.xinitrc.

3️⃣ Configurar Escalado en Wayland

Si decides usar Wayland, el escalado se maneja diferente:

Abre Preferencias del sistema.

Ve a Pantalla y monitor → Escalado de pantalla.

Ajusta la escala y aplica los cambios.

Si aún tienes problemas con aplicaciones que no respetan el escalado, puedes usar la variable de entorno:

export QT_SCALE_FACTOR=1.25
export GDK_SCALE=1.25

Añádelo a ~/.profile para que se aplique en cada inicio de sesión.

Soluciones para Problemas en Wayland en Kubuntu

Algunas aplicaciones pueden tener problemas en Wayland, especialmente aquellas que dependen de X11 para su renderizado (como algunas aplicaciones antiguas o ciertos programas propietarios). Si decides probar Wayland pero encuentras que algunas aplicaciones no funcionan bien, aquí hay soluciones alternativas para evitar problemas:

1️⃣ Ejecutar Aplicaciones en X11 Dentro de Wayland

Si una aplicación no funciona bien en Wayland, puedes forzarla a ejecutarse en X11 (XWayland) con este comando:

QT_QPA_PLATFORM=xcb nombre-del-programa

Ejemplo:

QT_QPA_PLATFORM=xcb firefox

Esto hará que Firefox se ejecute usando XWayland, solucionando problemas gráficos en algunas configuraciones.

2️⃣ Usar Variable Global para Todas las Aplicaciones Qt

Si muchas aplicaciones Qt tienen problemas, puedes hacer que todas se ejecuten en XWayland agregando esto en tu archivo ~/.profile:

export QT_QPA_PLATFORM=xcb

Luego, reinicia sesión para aplicar los cambios.

3️⃣ Usar PipeWire para Compartir Pantalla en Wayland

Si usas Zoom, Discord o Google Meet y no funciona la compartición de pantalla, instala PipeWire con:

sudo apt install pipewire wireplumber xdg-desktop-portal xdg-desktop-portal-kde

Luego reinicia el sistema.

4️⃣ Comprobar Soporte de Aplicaciones

Algunas apps pueden necesitar ajustes adicionales:

Firefox y Chrome → Habilita MOZ_ENABLE_WAYLAND=1 para mejor rendimiento en Wayland.

Electron apps (VS Code, Slack, Discord, etc.) → A veces tienen errores con Wayland, pero suelen funcionar bien con --enable-features=UseOzonePlatform --ozone-platform=wayland.

5️⃣ Si Nada Funciona Bien, Volver a X11

Si después de probar Wayland ves que muchas aplicaciones tienen problemas, puedes volver a X11 desde la pantalla de inicio de sesión:

Cierra sesión.

En la pantalla de inicio de sesión, selecciona Plasma (X11) en lugar de Plasma (Wayland).

Inicia sesión y verás que vuelves a usar X11.

Si deseas hacer X11 el predeterminado, ejecuta:

sudo update-alternatives --config x-session-manager

Y selecciona la opción de Plasma (X11).

Resumen

✅ Puedes ejecutar apps en X11 dentro de Wayland si tienen problemas.✅ Algunas apps pueden necesitar configuraciones extra.✅ PipeWire soluciona problemas de compartir pantalla.✅ Si Wayland no funciona bien, puedes volver a X11 fácilmente.

Prueba y ajusta según tus necesidades. 🚀

