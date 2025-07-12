# examentransversalmc

# productos = {modelo: [marca, pantalla, RAM, disco, GB de DD, procesador, videos], ...}
productos = {
    '8475HD': ['HP', 15.6, '8GB', 'DD', '1T', 'Intel Core i5', 'Nvidia GTX1050'],
    '2175HD': ['Acer', 14, '4GB', 'SSD', '512GB', 'Intel Core i5', 'Nvidia GTX1050'],
    'JjfFHD': ['Asus', 14, '16GB', 'SSD', '256GB', 'Intel Core i7', 'Nvidia RTX2080Ti'],
    'fgdxFHD': ['HP', 15.6, '12GB', 'DD', '1T', 'Intel Core i3', 'integrada'],
    'GF75HD': ['Asus', 15.6, '12GB', 'DD', '1T', 'Intel Core i7', 'Nvidia GTX1050'],
    '123FHD': ['Acer', 14, '6GB', 'DD', '1T', 'AMD Ryzen 5', 'integrada'],
    '342FHD': ['Acer', 15.6, '8GB', 'DD', '1T', 'AMD Ryzen 7', 'Nvidia GTX1050'],
    'UWU131HD': ['Dell', 15.6, '8GB', 'DD', '1T', 'AMD Ryzen 3', 'Nvidia GTX1050'],
}

stock = {
    "8475HD": [387990, 10],
    "2175HD": [327990, 4],
    "JjfFHD": [424990, 1],
    "123FHD": [290890, 32],
    "342FHD": [444990, 7],
    "UWU131HD": [349990, 1],
    "fgdxFHD": [664990, 21],
    "GF75HD": [749990, 2],
    "FS1230HD": [249990, 0]
}

# buscar stock por marca especificada
def stock_marca(marca):
    cantidad = 0
    for modelo, datos in productos.items():
        if datos[0].lower() == marca.lower():
            if modelo in stock:
                cantidad += stock[modelo][1]
    return cantidad

# eliminar producto
def eliminar_producto(modelo):
    if modelo in productos and modelo in stock:
        del productos[modelo]
        del stock[modelo]
        return True
    else:
        return False

# búsqueda por precios
def busqueda_precio(p_min, p_max):
    resultados = []
    for modelo, datos in stock.items():
        precio = datos[0]
        if p_min <= precio <= p_max:
            resultados.append(modelo)
    return resultados

# Menú principal
def menu_tiendapybooks():
    while True:
        print("\n*** MENU TIENDA PYBOOKS ***")
        print("1. Stock por marca.")
        print("2. Búsqueda por precio.")
        print("3. Eliminar producto.")
        print("4. Salir.")

        opcion = input("Ingrese opción: ")

        if opcion == "1":
            marca = input("Ingrese marca a consultar: ")
            cantidad = stock_marca(marca)
            print("El stock es: ", cantidad)

        elif opcion == '2':
            try:
                p_min = int(input("Ingrese precio mínimo: "))
                p_max = int(input("Ingrese precio máximo: "))
                resultados = busqueda_precio(p_min, p_max)
                if resultados:
                    print("Los notebooks entre los precios consultados son:", resultados)
                else:
                    print("No hay notebooks en ese rango de precios.")
            except ValueError:
                print("Debe ingresar valores enteros!!")

        elif opcion == "3":
            modelo = input("Ingrese modelo a eliminar: ")
            confirmar = input("¿Seguro que desea eliminarlo? (s/n): ")
            if confirmar == "s":
                exito = eliminar_producto(modelo)
                if exito:
                    print("Producto eliminado.")
                else:
                    print("Modelo no encontrado.")
            else:
                print("Cancelado.")

        elif opcion == "4":
            print("Programa finalizado. ¡Gracias!")
            break

        else:
            print("Debe seleccionar una opción válida!!")

# ejecutar menú
menu_tiendapybooks()
