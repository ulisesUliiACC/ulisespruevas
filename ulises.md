Ejercicio 1: Crear un CRUD Básico

Crea una aplicación Laravel para gestionar una lista de tareas. La aplicación debe permitir:

Crear una nueva tarea.
Listar todas las tareas.
Editar una tarea existente.
Eliminar una tarea.
Requisitos:
Migración para la tabla tasks:
php
Copiar código
// database/migrations/xxxx_xx_xx_create_tasks_table.php
Schema::create('tasks', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('description')->nullable();
    $table->boolean('completed')->default(false);
    $table->timestamps();
});
Modelo Task:
php
Copiar código
// app/Models/Task.php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    use HasFactory;

    protected $fillable = ['title', 'description', 'completed'];
}
Controlador TaskController:
php
Copiar código
// app/Http/Controllers/TaskController.php
namespace App\Http\Controllers;

use App\Models\Task;
use Illuminate\Http\Request;

class TaskController extends Controller
{
    public function index()
    {
        $tasks = Task::all();
        return view('tasks.index', compact('tasks'));
    }

    public function create()
    {
        return view('tasks.create');
    }

    public function store(Request $request)
    {
        Task::create($request->all());
        return redirect()->route('tasks.index');
    }

    public function edit(Task $task)
    {
        return view('tasks.edit', compact('task'));
    }

    public function update(Request $request, Task $task)
    {
        $task->update($request->all());
        return redirect()->route('tasks.index');
    }

    public function destroy(Task $task)
    {
        $task->delete();
        return redirect()->route('tasks.index');
    }
}
Rutas:
php
Copiar código
// routes/web.php
use App\Http\Controllers\TaskController;

Route::resource('tasks', TaskController::class);

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página Responsiva</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
</head>
<body>
    <header>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#">Mi Sitio</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Inicio <span class="sr-only">(current)</span></a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Contacto</a>
                    </li>
                </ul>
            </div>
        </nav>
    </header>
    <main class="container mt-5">
        <h1>Formulario de Contacto</h1>
        <form>
            <div class="form-group">
                <label for="name">Nombre</label>
                <input type="text" class="form-control" id="name" placeholder="Nombre">
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" class="form-control" id="email" placeholder="Email">
            </div>
            <div class="form-group">
                <label for="message">Mensaje</label>
                <textarea class="form-control" id="message" rows="3"></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Enviar</button>
        </form>
    </main>
    <footer class="bg-light text-center py-3 mt-5">
        <p>&copy; 2024 Mi Sitio</p>
    </footer>
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
Escribe una consulta SQL para obtener todos los clientes de una tabla customers que viven en 'New York'.
sql
Copiar código
SELECT * FROM customers WHERE city = 'New York';
Escribe una consulta SQL para obtener el nombre del cliente y el número de pedido de las tablas orders y customers.
sql
Copiar código
SELECT customers.name, orders.order_number 
FROM orders 
INNER JOIN customers ON orders.customer_id = customers.id;
JavaScript
Ejercicio 4: Manipulación del DOM y AJAX

Escribe un script que cambie el contenido de un elemento con el id demo al texto "Hola Mundo" cuando se haga clic en un botón.
html
Copiar código
<button onclick="changeText()">Click me</button>
<p id="demo">Texto original</p>

<script>
function changeText() {
  document.getElementById("demo").innerHTML = "Hola Mundo";
}
</script>
Escribe una función que realice una solicitud AJAX a una API y muestre los datos recibidos en la consola.
html
Copiar código
<script>
function fetchData() {
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
}
fetchData();
</script>
Java
Ejercicio 5: Clases y Herencia

Crea una clase Persona con los atributos nombre y edad. Luego, crea un objeto de esa clase y muestra sus atributos.
java
Copiar código
public class Persona {
    String nombre;
    int edad;

    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    public static void main(String[] args) {
        Persona persona = new Persona("Juan", 30);
        System.out.println("Nombre: " + persona.nombre);
        System.out.println("Edad: " + persona.edad);
    }
}
Crea una clase Empleado que herede de la clase Persona y agregue un atributo salario. Muestra los atributos del objeto Empleado.
java
Copiar código
public class Empleado extends Persona {
    double salario;

    public Empleado(String nombre, int edad, double salario) {
        super(nombre, edad);
        this.salario = salario;
    }

    public static void main(String[] args) {
        Empleado empleado = new Empleado("Ana", 28, 50000);
        System.out.println("Nombre: " + empleado.nombre);
        System.out.println("Edad: " + empleado.edad);
        System.out.println("Salario: " + empleado.salario);
    }
}
Estos ejercicios te proporcionarán una buena práctica en las tecnologías que mencionaste. Te recomiendo que los completes y pruebes tu código en un entorno de desarrollo real. ¡Buena suerte en tu prueba técnica!

como cconsumir una api en laravel

ChatGPT
Consumir una API externa en Laravel es un proceso común que puede ser manejado eficientemente utilizando la biblioteca GuzzleHTTP, que viene preinstalada con Laravel. Aquí tienes una guía paso a paso para consumir una API en Laravel:

Paso 1: Configurar GuzzleHTTP
Laravel proporciona una forma sencilla de trabajar con GuzzleHTTP a través del cliente HTTP que viene preconfigurado. Puedes utilizar este cliente directamente o configurar Guzzle en el archivo config/services.php si necesitas configuraciones específicas.

Paso 2: Crear un Servicio para la API
Es una buena práctica crear un servicio dedicado para manejar la interacción con la API externa. Esto ayuda a mantener el código organizado y facilita su mantenimiento.

Crear el servicio: Puedes crear un nuevo servicio usando el comando make de Artisan para generar una clase donde se manejarán las llamadas a la API.
bash
Copiar código
php artisan make:service ApiService
Definir el servicio:
php
Copiar código
// app/Services/ApiService.php
namespace App\Services;

use Illuminate\Support\Facades\Http;

class ApiService
{
    protected $baseUrl;

    public function __construct()
    {
        $this->baseUrl = 'https://api.example.com'; // Reemplaza con la URL base de la API que estás consumiendo
    }

    public function getData($endpoint)
    {
        $response = Http::get($this->baseUrl . '/' . $endpoint);

        if ($response->successful()) {
            return $response->json();
        }

        return null; // Maneja errores según sea necesario
    }
}
Paso 3: Usar el Servicio en un Controlador
Ahora, puedes utilizar este servicio en tus controladores para consumir la API.

Crear un controlador: Si no tienes un controlador, créalo usando Artisan.
bash
Copiar código
php artisan make:controller ApiController
Utilizar el servicio en el controlador:
php
Copiar código
// app/Http/Controllers/ApiController.php
namespace App\Http\Controllers;

use App\Services\ApiService;

class ApiController extends Controller
{
    protected $apiService;

    public function __construct(ApiService $apiService)
    {
        $this->apiService = $apiService;
    }

    public function index()
    {
        $data = $this->apiService->getData('some-endpoint'); // Reemplaza 'some-endpoint' con el endpoint real

        return view('api.index', compact('data')); // Pasa los datos a una vista
    }
}
Paso 4: Crear una Vista para Mostrar los Datos
Crear la vista: Crea una vista en resources/views/api/index.blade.php para mostrar los datos.
php
Copiar código
<!-- resources/views/api/index.blade.php -->
<!DOCTYPE html>
<html>
<head>
    <title>API Data</title>
</head>
<body>
    <h1>Datos de la API</h1>
    @if ($data)
        <ul>
            @foreach ($data as $item)
                <li>{{ $item['name'] }}</li> <!-- Ajusta según la estructura de datos de la API -->
            @endforeach
        </ul>
    @else
        <p>No se encontraron datos.</p>
    @endif
</body>
</html>
Paso 5: Configurar la Ruta
Configurar una ruta: Añade una ruta en routes/web.php para acceder al controlador.
php
Copiar código
// routes/web.php
use App\Http\Controllers\ApiController;

Route::get('/api-data', [ApiController::class, 'index']);
