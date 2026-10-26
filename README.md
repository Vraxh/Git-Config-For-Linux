# 🐧 Configuración de Git y GitHub

Guía basada en la lección oficial de **The Odin Project** para la instalación, configuración global y autenticación SSH de Git con GitHub en Linux.

---

## 📋 Descripción General
En esta guía aprenderás a:
* Instalar Git en Linux.
* Crear y configurar tu cuenta de GitHub de forma segura.
* Configurar los datos de usuario global en Git.
* Establecer la rama predeterminada como `main`.
* Generar y asociar una clave SSH con GitHub para trabajar sin ingresar contraseñas constantemente.

---

## 🛠️ Paso 1: Instalar Git

Abre tu terminal e instala Git según la distribución de Linux que utilices:

* **Ubuntu / Debian / Linux Mint:**
  ```bash
  sudo apt update
  sudo apt install git
  ```

* **Fedora / RHEL / CentOS:**
  ```bash
  sudo dnf install git
  ```

* **Arch Linux:**
  ```bash
  sudo pacman -S git
  ```

Para verificar que la instalación fue exitosa:
```bash
git --version
```

---

## ⚙️ Paso 2: Configuración de Cuenta en GitHub

1. Ingresa a [GitHub.com](https://github.com) y crea una cuenta con tu correo electrónico.
2. **(Recomendado por privacidad):** Para evitar exponer tu correo personal públicamente en tus confirmaciones (*commits*):
   * Ve a **Settings > Emails**.
   * Activa las opciones:
     * *Keep my email addresses private*
     * *Block command line pushes that expose my email*
   * Toma nota del correo privado generado por GitHub (ejemplo: `123456789+username@users.noreply.github.com`).

---

## 👤 Paso 3: Configuración Global de Git

Ejecuta los siguientes comandos en tu terminal. Asegúrate de incluir las comillas:

### 1. Establecer tu nombre y correo
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@example.com"
```
*(Si decidiste ocultar tu correo en GitHub, utiliza la dirección privada `@users.noreply.github.com` en lugar de tu correo personal).*

### 2. Definir `main` como la rama por defecto
```bash
git config --global init.defaultBranch main
```

### 3. Verificar la configuración
```bash
git config --get user.name
git config --get user.email
```

---

## 🔑 Paso 4: Crear y Configurar Clave SSH

La clave SSH te permitirá conectarte e interactuar con tus repositorios en GitHub sin escribir tu contraseña en cada operación.

### 1. Comprobar si ya existe una clave SSH
```bash
ls ~/.ssh/id_ed25519.pub
```
* Si la terminal responde `No such file or directory`, continúa al siguiente punto.
* Si el archivo ya existe, puedes saltar directo a la sección de copiar la clave.

### 2. Generar una nueva clave SSH (Ed25519)
```bash
ssh-keygen -t ed25519
```
* Cuando te pregunte la ubicación de guardado (`Enter file in which to save...`), presiona **Enter** para aceptar la ruta por defecto.
* Cuando te pida una frase de paso (*passphrase*), puedes presionar **Enter** dos veces si no deseas añadir una contraseña adicional.

---

## 🔗 Paso 5: Vincular la Clave SSH con GitHub

### 1. Mostrar y copiar tu clave pública
Ejecuta el siguiente comando para ver el contenido de tu clave SSH pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

Selecciona y copia todo el texto impreso en la terminal (comienza con `ssh-ed25519` y termina con tu usuario/host).

### 2. Agregar la clave a tu cuenta de GitHub
1. Inicia sesión en GitHub y haz clic en tu foto de perfil (esquina superior derecha).
2. Selecciona **Settings**.
3. En el menú lateral izquierdo, haz clic en **SSH and GPG keys**.
4. Haz clic en el botón verde **New SSH Key**.
5. En el campo **Title**, escribe un nombre descriptivo para identificar tu equipo (ejemplo: `linux-laptop`).
6. Deja el tipo de clave como **Authentication Key**.
7. En el campo **Key**, pega la clave que copiaste en la terminal.
8. Haz clic en **Add SSH key**.

---

## 🧪 Paso 6: Verificar la Conexión SSH

Para corroborar que todo esté correctamente vinculado, ejecuta en tu terminal:

```bash
ssh -T git@github.com
```

Si es la primera vez que te conectas, la terminal te preguntará si deseas continuar (`Are you sure you want to continue connecting (yes/no/[fingerprint])?`). Escribe `yes` y presiona **Enter**.

Deberías recibir la siguiente respuesta exitosa:
> *Hi username! You've successfully authenticated, but GitHub does not provide shell access.*

¡Felicidades! Tu entorno local de Git y tu cuenta de GitHub ya están configurados y listos para trabajar.