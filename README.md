# Configuración de Django con Docker y Docker Compose

Este repositorio proporciona una configuración básica para ejecutar una aplicación Django utilizando Docker y Docker Compose.

## Instalación

Sigue estos pasos para configurar y ejecutar la aplicación Django con Docker:

1. **Clona el repositorio:**

	```bash
	git clone <URL_del_repositorio>
	```

2. **Crea el archivo `.env.dev`:**

	Crea un archivo llamado `.env.dev` en la raíz del proyecto y define las variables de entorno necesarias. Aquí tienes un ejemplo:

	```dotenv
	DEBUG=1
	SECRET_KEY=your_secret_key
	DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]
	```

  Asegúrate de cambiar `your_secret_key` por una clave secreta segura.

3. **Construye y levanta los contenedores de Docker:**

	```bash
	docker-compose up -d --build
	```

	Este comando construirá las imágenes de Docker según el Dockerfile y docker-compose.yml proporcionados, y luego iniciará los contenedores en segundo plano.

4. **Aplica las migraciones de Django:**

	Accede al contenedor de Django y aplica las migraciones de Django:

	```bash
	docker-compose exec web python manage.py migrate
	```

5. **Crea un superusuario (opcional):**

	Si deseas acceder al panel de administración de Django, puedes crear un superusuario ejecutando el siguiente comando:

	```bash
	docker-compose exec web python manage.py createsuperuser
	```

6. **Accede a la aplicación:**

	Una vez que todos los contenedores estén en funcionamiento, podrás acceder a tu aplicación Django en `http://localhost:8000`.

## Archivos de configuración

### Dockerfile

El Dockerfile define la configuración para construir la imagen de Docker para la aplicación Django. Instala las dependencias del sistema, copia el código fuente de la aplicación, y configura el contenedor para ejecutar el script `entrypoint.sh` al iniciarse.

### docker-compose.yml

El archivo docker-compose.yml define los servicios necesarios para ejecutar la aplicación, incluyendo el servicio web de Django y el servicio de base de datos PostgreSQL. Configura las dependencias entre los servicios y especifica las variables de entorno necesarias.

## Variables de entorno

### .env.dev

El archivo `.env.dev` contiene las variables de entorno específicas de desarrollo para la aplicación Django, como la configuración de depuración, la clave secreta y los hosts permitidos.

Asegúrate de no incluir este archivo en tu repositorio público, ya que puede contener información sensible.

