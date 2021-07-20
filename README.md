### Instalación

1. Instalar dependencias de PHP `composer install`
2. Crear el archivo .env usando de ejemplo el .env.example
3. Generar el key del framework en la raíz del proyecto `php artisan key:generate`
4. Correr las migraciones para crear las tablas necesarias `php artisan migrate`
5. Instalar las dependencias que usara el node para el front (VueJs) `npm install`
6. Compilar el front del VueJs `npm run development`

### Dashboard Products

- Se crearon las migraciones necesarias para todo el auth
- Se creó un Rest Api para registrar usuarios y para logear usuarios este login retorna un bearer token para usar las apis que lo requieran, se realizó usando passport, esta retornara code 400 bad request junto al mensaje en caso de enviar mal los parámetros o no pasar las validaciones los mismos
- Se creó auth del proyecto con oauth
- Se crearon vistas para todo el auth y un home (Dashboard Products) que solo es accesible si se está logeado
- La vista para registrar un nuevo usuario se creó en VueJs y se integró con Axios el ApiRest de registro de usuario creado anteriormente con passport 
- Una vez logeado, el middleware permitirá acceder al home (Dashboard Products)  
