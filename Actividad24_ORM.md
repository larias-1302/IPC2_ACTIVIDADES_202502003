# Actividad Corta de Laboratorio: De ADO.NET Tradicional a la Automatización con EF Core

## Parte 1: Diagnóstico Técnico y Brecha de Impedancia

### Serie 1

La brecha de impedancia es la diferencia entre la forma en que los lenguajes orientados a objetos representan la información y la forma en que las bases de datos relacionales la almacenan.

* **Clase Clásica (POCO)** → **Tabla**
* **Propiedad/Atributo** → **Columna**
* **Instancia de Objeto** → **Fila (Registro)**

### Serie 2

Entity Framework Core previene automáticamente la Inyección SQL mediante el uso de consultas parametrizadas, evitando que los datos del usuario se concatenen directamente en la consulta SQL.

En ADO.NET tradicional esto se mitigaba utilizando parámetros, por ejemplo:

```csharp
cmd.Parameters.AddWithValue("@filtro", "Ing.%");
```

### Serie 3

El método `.AsNoTracking()` mejora el rendimiento porque desactiva el seguimiento de cambios de las entidades consultadas. Esto reduce el consumo de memoria RAM y de recursos del servidor, siendo ideal para consultas que solo muestran información y no requieren modificaciones.

---

## Parte 2: Desafío de Refactorización de Código

### Serie 1

```csharp
using Microsoft.EntityFrameworkCore;

public class UnidadAcademicaContext : DbContext
{
    public UnidadAcademicaContext(DbContextOptions<UnidadAcademicaContext> options)
        : base(options)
    {
    }

    public DbSet<Catedratico> Catedraticos { get; set; }
}
```

### Serie 2

```csharp
using Microsoft.EntityFrameworkCore;

public class CatedraticoService
{
    private readonly UnidadAcademicaContext _context;

    public CatedraticoService(UnidadAcademicaContext context)
    {
        _context = context;
    }

    public List<Catedratico> ObtenerCatedraticos()
    {
        return _context.Catedraticos
            .AsNoTracking()
            .Where(c => c.Nombre.StartsWith("Ing."))
            .ToList();
    }
}
```

---

## Parte 3: Referencias Bibliográficas

* Facultad de Ingeniería, USAC. (2026). *Sesión 17: Conectividad con SQL Server. Acceso Estructurado a Datos mediante C# y ADO.NET.* Laboratorio de Introducción a la Programación y Computación 2. Guatemala.

* Facultad de Ingeniería, USAC. (2026). *Sesión 18: Mapeo de Objetos Relacionales. Persistencia Automatizada con Entity Framework Core.* Laboratorio de Introducción a la Programación y Computación 2. Guatemala.
