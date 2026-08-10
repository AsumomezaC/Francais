---
tags:
  - Obsidian
  - Terminal
  - git
---
# 🚀 Configuración de GitHub, Termux y Obsidian en Android

Esta guía detalla el proceso para sincronizar repositorios de GitHub con Obsidian en Android mediante Termux, configurando llaves SSH y automatizando la subida de cambios por materias o de forma global.

---

## 1. Instalación de Termux

> [!WARNING] No instalar desde Google Play
> La versión de Google Play está desactualizada y no puede descargar paquetes. Usar la versión de **F-Droid**.

1. Descargar la APK de **F-Droid** desde su sitio oficial o instalar directamente el APK de Termux desde [f-droid.org](https://f-droid.org/packages/com.termux/).
2. Abrir **Termux** y ejecutar el comando para actualizar los repositorios base:
```bash
   pkg update && pkg upgrade -y
```

3. Conceder permisos de acceso al almacenamiento interno de la tablet:
``` Bash
    termux-setup-storage
```
>_(Aceptar la ventana emergente de permisos de Android)_.


## 2. Configuración de Git y Clave SSH

1. Instalar **Git** y **OpenSSH** dentro de Termux:
``` Bash
    pkg install git openssh -y
```

2. Configurar la identidad global de Git:
``` Bash
    git config --global user.name "TuNombre"
    git config --global user.email "tu_email@ejemplo.com"
```

3. Generar la clave SSH utilizando el algoritmo de curva elíptica `ed25519`:
``` Bash
    ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```
>_(Presionar `Enter` a todas las preguntas para usar las rutas por defecto y dejar sin contraseña)_.

> [!NOTE] ¿Por qué `ed25519`?
> 
> Es un algoritmo moderno, ligero para el procesador de la tablet, altamente seguro y genera claves más cortas, ideales para copiar y pegar.
> 
>   

## 3. Vinculación de la Clave SSH en GitHub

1. Mostrar la clave pública completa en la pantalla de Termux:
```Bash
    cat ~/.ssh/id_ed25519.pub
```

2. **Copiar la línea completa**, asegurándote de incluir las tres partes:
    - El inicio: `ssh-ed25519`
    - El cuerpo cifrado: `AAAAC3NzaC...`
    - El correo final: `tu_email@ejemplo.com`

3. Ir a **GitHub.com** → **Settings** → **SSH and GPG keys** → **New SSH key**.

4. Asignar un nombre (ej. _Tablet Android_) y pegar el contenido.

5. Probar la conexión desde Termux:
```Bash
    ssh-T git@github.com
```
>_(Escribir `yes` si solicita confirmación)._
## 4. Clonar el Repositorio
1. Navegar al almacenamiento compartido de la tablet (Ruta real de Android: `/storage/emulated/0/`):
```Bash
    cd ~/storage/shared/
```

2. Crear la carpeta principal de tu bóveda (si no existe):
```Bash
    mkdir MisNotas && cd MisNotas
```

3. Clonar el repositorio deseado mediante SSH -haz esto por cada repositorio que quieras clonar-:
``` Bash
    git clone git@github.com:tu_usuario/tu_repositorio.git
```
## 5. Abrir la Bóveda en Obsidian

1. Abrir **Obsidian**.
2. Si te encuentras dentro de una bóveda vacía: Ir a **Ajustes (⚙️)** → **Gestionar Bóvedas** (o presionar `Ctrl + P` / Deslizar consola y `Abrir otra bóveda`).
3. Seleccionar **Abrir carpeta existente como bóveda** (_Open folder as vault_).
4. Navegar a **Almacenamiento interno** → `MisNotas` y seleccionar la carpeta de la materia.
## 6. Script de Sincronización Automatizado
Para gestionar múltiples repositorios (carpetas de distintas materias como `Frances`, `Ingles`, etc.) dentro de la misma bóveda `MisNotas`, se utiliza un script Bash interactivo.
### Crear el script `sync.sh`:
Ejecutar el siguiente bloque en Termux:

``` Bash
cat << 'EOF' > ~/sync.sh
#!/bin/bash

# Ruta principal de tu bóveda en Android
VAULT_DIR="$HOME/storage/shared/MisNotas"

sync_repo() {
    local repo_path="$1"
    local repo_name=$(basename "$repo_path")

    if [ -d "$repo_path/.git" ]; then
        echo "---------------------------------"
        echo "📂 Sincronizando: $repo_name"
        cd "$repo_path" || return

        git add .
        
        if ! git diff-index --quiet HEAD -- 2>/dev/null; then
            git commit -m "Auto-sync ($repo_name): $(date +'%Y-%m-%d %H:%M')"
            echo "📝 Cambios guardados localmente."
        else
            echo "💤 Sin cambios pendientes."
        fi

        BRANCH=$(git branch --show-current)
        git pull --rebase origin "$BRANCH"
        git push origin "$BRANCH"
        echo "🚀 ¡$repo_name subido correctamente a GitHub!"
    else
        echo "⚠️ La carpeta '$repo_name' no existe o no es un repositorio de Git."
    fi
}

TARGET="$1"

if [ -z "$TARGET" ] || [ "$TARGET" = "all" ]; then
    for dir in "$VAULT_DIR"/*/; do
        sync_repo "$dir"
    done
else
    sync_repo "$VAULT_DIR/$TARGET"
fi
EOF

chmod +x ~/sync.sh
```

### Crear el Alias de acceso rápido:
``` Bash
echo "alias sync='~/sync.sh'" >> ~/.bashrc && source ~/.bashrc
```
### 🎮 Formas de uso:

- **Sincronizar una carpeta específica:**
``` Bash
    sync Frances
    sync Ingles
```

- **Sincronizar TODOS los repositorios a la vez:**
``` Bash
    sync
```
## 7. Alternativa: Sincronización Automática cada "X" tiempo (Cron)
Si prefieres no ejecutar el comando manualmente y deseas que el script se corra solo en segundo plano:
1. Instalar el gestor de tareas `cronie`:
``` Bash
    pkg install cronie -y
```

2. Abrir el editor de tareas programadas:
``` Bash
    crontab -e
```

3. Agregar la siguiente regla al final del archivo (Ejemplo para ejecutar **cada 30 minutos**):
```
    */30 * * * * ~/sync.sh > /dev/null 2>&1
```
>_(Si deseas que sea cada hora, cambia `*/30` por `0`)._

4. Iniciar el demonio de automatización en Termux:
``` Bash
    crond
```