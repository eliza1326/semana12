
link ejecutable: https://www.programiz.com/online-compiler/3UmPgCfoLZ7vu
# semana12
using System;
using System.Collections.Generic;

class Libro
{
    public string Titulo { get; set; }
    public string Autor { get; set; }
    public int AnioPublicacion { get; set; }

    public Libro(string titulo, string autor, int anioPublicacion)
    {
        Titulo = titulo;
        Autor = autor;
        AnioPublicacion = anioPublicacion;
    }

    public override string ToString()
    {
        return $"Título: {Titulo}, Autor: {Autor}, Año: {AnioPublicacion}";
    }
}

class Biblioteca
{
    private Dictionary<string, Libro> libros = new Dictionary<string, Libro>();

    public void AgregarLibro(Libro libro)
    {
        if (!libros.ContainsKey(libro.Titulo))
        {
            libros[libro.Titulo] = libro;
            Console.WriteLine("Libro agregado correctamente.");
        }
        else
        {
            Console.WriteLine("El libro ya existe en la biblioteca.");
        }
    }

    public void MostrarLibros()
    {
        if (libros.Count == 0)
        {
            Console.WriteLine("No hay libros registrados.");
            return;
        }
        Console.WriteLine("\nLista de libros en la biblioteca:");
        foreach (var libro in libros.Values)
        {
            Console.WriteLine(libro);
        }
    }

    public void BuscarLibroPorTitulo(string titulo)
    {
        if (libros.ContainsKey(titulo))
        {
            Console.WriteLine("\nLibro encontrado:");
            Console.WriteLine(libros[titulo]);
        }
        else
        {
            Console.WriteLine("Libro no encontrado.");
        }
    }
}

class Program
{
    static void Main()
    {
        Biblioteca biblioteca = new Biblioteca();

        while (true)
        {
            Console.WriteLine("\nMenú de Biblioteca");
            Console.WriteLine("1. Agregar libro");
            Console.WriteLine("2. Mostrar libros");
            Console.WriteLine("3. Buscar libro por título");
            Console.WriteLine("4. Salir");
            Console.Write("Seleccione una opción: ");
            
            int opcion;
            if (!int.TryParse(Console.ReadLine(), out opcion))
            {
                Console.WriteLine("Opción no válida, intente de nuevo.");
                continue;
            }

            switch (opcion)
            {
                case 1:
                    Console.Write("Ingrese el título del libro: ");
                    string titulo = Console.ReadLine();
                    Console.Write("Ingrese el autor del libro: ");
                    string autor = Console.ReadLine();
                    Console.Write("Ingrese el año de publicación: ");
                    int anio;
                    if (!int.TryParse(Console.ReadLine(), out anio))
                    {
                        Console.WriteLine("Año no válido.");
                        break;
                    }
                    biblioteca.AgregarLibro(new Libro(titulo, autor, anio));
                    break;
                case 2:
                    biblioteca.MostrarLibros();
                    break;
                case 3:
                    Console.Write("Ingrese el título del libro a buscar: ");
                    string busqueda = Console.ReadLine();
                    biblioteca.BuscarLibroPorTitulo(busqueda);
                    break;
                case 4:
                    Console.WriteLine("Saliendo...");
                    return;
                default:
                    Console.WriteLine("Opción no válida, intente de nuevo.");
                    break;
            }
        }
    }
}
