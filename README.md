# IS1-Cotizaciones

# Sistema de Cotizaciones

## Descripción
Sistema de gestión de cotizaciones desarrollado con Spring Boot siguiendo principios de Domain Driven Design (DDD). Permite gestionar cotizaciones de productos y servicios con funcionalidades completas de CRUD y reportería.

## Propósito
Facilitar el proceso de creación, gestión y seguimiento de cotizaciones comerciales, proporcionando una interfaz intuitiva y un backend robusto para el manejo de datos empresariales.

## Tecnologías Utilizadas
- **Backend**: Spring Boot 3.x
- **Base de Datos**: H2 (desarrollo) / MySQL (producción)
- **ORM**: Spring Data JPA
- **Build Tool**: Maven
- **IDE**: Visual Studio Code
- **Control de Versiones**: Git & GitHub
- **Arquitectura**: Domain Driven Design (DDD)

## Estructura del Proyecto
```
src/
├── main/
│   ├── java/com/example/cotizaciones/
│   │   ├── cotizaciones/          # Entidades principales
│   │   ├── domain/               # Modelo de dominio
│   │   ├── controller/           # Capa de presentación
│   │   ├── service/              # Lógica de negocio
│   │   └── repository/           # Acceso a datos
│   └── resources/
│       ├── application.properties
│       └── static/
└── test/
```

## Funcionalidades de Alto Nivel

### Diagrama de Casos de Uso UML
```
[Cliente] ──── (Crear Cotización)
    │
    ├──── (Consultar Cotizaciones)
    │
    ├──── (Modificar Cotización)
    │
    ├──── (Eliminar Cotización)
    │
    └──── (Generar Reporte)

[Administrador] ──── (Gestionar Productos)
    │
    ├──── (Configurar Precios)
    │
    └──── (Administrar Usuarios)
```

### Prototipo (GUI)
**Pantalla Principal de Cotizaciones:**
- Lista de cotizaciones con filtros por fecha, cliente y estado
- Botones de acción: Crear, Editar, Eliminar, Ver Detalles
- Barra de búsqueda y paginación

**Formulario de Cotización:**
- Datos del cliente (nombre, email, teléfono)
- Selección de productos/servicios
- Cantidades y precios unitarios
- Cálculo automático de totales e impuestos
- Botones: Guardar, Cancelar, Vista Previa

## Modelo de Dominio

### Diagrama de Clases + Módulos

#### Módulo de Cotizaciones
```java
@Entity
public class Cotizacion {
    @Id
    private Long id;
    private String numero;
    private LocalDate fecha;
    private EstadoCotizacion estado;
    
    @ManyToOne
    private Cliente cliente;
    
    @OneToMany(mappedBy = "cotizacion")
    private List<DetalleCotizacion> detalles;
}

@Entity
public class DetalleCotizacion {
    @Id
    private Long id;
    private Integer cantidad;
    private BigDecimal precioUnitario;
    
    @ManyToOne
    private Producto producto;
    
    @ManyToOne
    private Cotizacion cotizacion;
}
```

#### Módulo de Clientes
```java
@Entity
public class Cliente {
    @Id
    private Long id;
    private String nombre;
    private String email;
    private String telefono;
    private String direccion;
}
```

#### Módulo de Productos
```java
@Entity
public class Producto {
    @Id
    private Long id;
    private String codigo;
    private String nombre;
    private String descripcion;
    private BigDecimal precio;
    private String categoria;
}
```

## Vista General de Arquitectura

### Diagrama de Paquetes + Clases
```
┌─────────────────────────────────────┐
│           PRESENTATION              │
│  ┌─────────────────────────────┐   │
│  │    CotizacionController     │   │
│  │    ClienteController        │   │
│  │    ProductoController       │   │
│  └─────────────────────────────┘   │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│             SERVICE                 │
│  ┌─────────────────────────────┐   │
│  │    CotizacionService        │   │
│  │    ClienteService           │   │
│  │    ProductoService          │   │
│  └─────────────────────────────┘   │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│            REPOSITORY               │
│  ┌─────────────────────────────┐   │
│  │    CotizacionRepository     │   │
│  │    ClienteRepository        │   │
│  │    ProductoRepository       │   │
│  └─────────────────────────────┘   │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│             DOMAIN                  │
│  ┌─────────────────────────────┐   │
│  │    Cotizacion               │   │
│  │    Cliente                  │   │
│  │    Producto                 │   │
│  │    DetalleCotizacion        │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

## Instalación y Configuración

### Prerrequisitos
- Java 17 o superior
- Maven 3.6+
- IDE (VSCode recomendado)
- Git

### Pasos de Instalación
1. Clonar el repositorio:
```bash
git clone https://github.com/irh1n0c/IS1-Cotizaciones.git
cd IS1-Cotizaciones
```

2. Compilar el proyecto:
```bash
mvn clean compile
```

3. Ejecutar la aplicación:
```bash
mvn spring-boot:run
```

4. Acceder a la aplicación:
```
http://localhost:8080
```

## Uso
1. Crear nuevos clientes desde el módulo de administración
2. Registrar productos con sus respectivos precios
3. Generar cotizaciones seleccionando cliente y productos
4. Gestionar el estado de las cotizaciones (borrador, enviada, aprobada)
5. Exportar cotizaciones a PDF

## Contribución
1. Fork del proyecto
2. Crear rama feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crear Pull Request

## Licencia
Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE.md](LICENSE.md) para detalles.

## Autor
- **IS1** - https://github.com/irh1n0c/IS1-Cotizaciones

## Estado del Proyecto
🚧 En desarrollo activo