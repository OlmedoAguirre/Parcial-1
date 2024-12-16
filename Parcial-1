import sqlite3

# Configuración de la base de datos
db_name = "presupuesto.db"

def inicializar_bd():
    """Crea la tabla de artículos si no existe."""
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS articulos (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nombre TEXT NOT NULL,
            descripcion TEXT,
            costo REAL NOT NULL
        )
    """)
    conexion.commit()
    conexion.close()

# Funciones
def registrar_articulo():
    nombre = input("Ingrese el nombre del artículo: ").strip()
    descripcion = input("Ingrese una descripción: ").strip()
    costo = float(input("Ingrese el costo: "))
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("INSERT INTO articulos (nombre, descripcion, costo) VALUES (?, ?, ?)", (nombre, descripcion, costo))
    conexion.commit()
    conexion.close()
    print("Artículo registrado exitosamente.\n")

def buscar_articulo():
    nombre = input("Ingrese el nombre del artículo a buscar: ").strip()
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("SELECT * FROM articulos WHERE nombre LIKE ?", (f"%{nombre}%",))
    resultados = cursor.fetchall()
    conexion.close()
    if resultados:
        print("\nArtículos encontrados:")
        for articulo in resultados:
            print(f"{articulo[0]}. {articulo[1]} - {articulo[2]} - ${articulo[3]:.2f}")
    else:
        print("No se encontraron artículos con ese nombre.\n")

def editar_articulo():
    articulo_id = int(input("Ingrese el ID del artículo a editar: "))
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("SELECT * FROM articulos WHERE id = ?", (articulo_id,))
    articulo = cursor.fetchone()
    if articulo:
        print(f"Editando artículo: {articulo[1]}")
        nuevo_nombre = input("Nuevo nombre (deje en blanco para mantener): ").strip() or articulo[1]
        nueva_descripcion = input("Nueva descripción (deje en blanco para mantener): ").strip() or articulo[2]
        nuevo_costo = input("Nuevo costo (deje en blanco para mantener): ").strip()
        nuevo_costo = float(nuevo_costo) if nuevo_costo else articulo[3]
        cursor.execute("""
            UPDATE articulos
            SET nombre = ?, descripcion = ?, costo = ?
            WHERE id = ?
        """, (nuevo_nombre, nueva_descripcion, nuevo_costo, articulo_id))
        conexion.commit()
        print("Artículo editado exitosamente.\n")
    else:
        print("No se encontró un artículo con ese ID.\n")
    conexion.close()

def eliminar_articulo():
    articulo_id = int(input("Ingrese el ID del artículo a eliminar: "))
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("DELETE FROM articulos WHERE id = ?", (articulo_id,))
    if cursor.rowcount > 0:
        print("Artículo eliminado exitosamente.\n")
    else:
        print("No se encontró un artículo con ese ID.\n")
    conexion.commit()
    conexion.close()

def mostrar_articulos():
    conexion = sqlite3.connect(db_name)
    cursor = conexion.cursor()
    cursor.execute("SELECT * FROM articulos")
    articulos = cursor.fetchall()
    conexion.close()
    if articulos:
        print("\nArtículos registrados:")
        for articulo in articulos:
            print(f"{articulo[0]}. {articulo[1]} - {articulo[2]} - ${articulo[3]:.2f}")
        print()
    else:
        print("No hay artículos registrados.\n")

# Menú principal
def menu():
    inicializar_bd()
    while True:
        print("=== Sistema de Registro de Presupuesto ===")
        print("1. Registrar artículo")
        print("2. Buscar artículo")
        print("3. Editar artículo")
        print("4. Eliminar artículo")
        print("5. Mostrar todos los artículos")
        print("6. Salir")
        opcion = input("Seleccione una opción: ").strip()

        if opcion == "1":
            registrar_articulo()
        elif opcion == "2":
            buscar_articulo()
        elif opcion == "3":
            editar_articulo()
        elif opcion == "4":
            eliminar_articulo()
        elif opcion == "5":
            mostrar_articulos()
        elif opcion == "6":
            print("Saliendo del programa...")
            break  # Salir del bucle principal
        else:
            print("Opción no válida. Intente nuevamente.\n")

# Ejecutar el programa
if __name__ == "__main__":
    menu()
