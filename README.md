#include <stdio.h>

int main() {
    char id[100], nombre[100];
    int cantidad_stock = 0, cantidad, opcion, producto_registrado = 0;
    float precio_unitario = 0, ganancias = 0, gastos = 0, total_ganancias = 0, total_gastos = 0;

    do {
        printf("\n=== Menu ===\n");
        printf("1. Agregar producto\n");
        printf("2. Vender producto\n");
        printf("3. Reabastecer producto\n");
        printf("4. Consultar informacion\n");
        printf("5. Calcular ganancias y gastos\n");
        printf("6. Salir\n");
        printf("Seleccione una opcion: ");

        if (scanf("%d", &opcion) != 1) {
            printf("Opcion invalida. Intente de nuevo.\n");
            while (getchar() != '\n');
            continue;
        }
        getchar();

        if (opcion == 1) {
            if (producto_registrado) {
                printf("Ya se ha agregado un producto. No puede agregar mas.\n");
                continue;
            }

            printf("Ingrese el ID del producto: ");
            fgets(id, sizeof(id), stdin);
            printf("Ingrese el nombre del producto: ");
            fgets(nombre, sizeof(nombre), stdin);
            printf("Ingrese la cantidad en stock: ");
            scanf("%d", &cantidad_stock);
            printf("Ingrese el precio unitario: ");
            scanf("%f", &precio_unitario);
            getchar();

            producto_registrado = 1;
            printf("Producto agregado con exito.\n");
        }

        if (opcion == 2) {
            if (!producto_registrado) {
                printf("No hay productos registrados. Agregue un producto primero.\n");
                continue;
            }

            printf("Ingrese la cantidad de producto a vender: ");
            scanf("%d", &cantidad);

            if (cantidad > cantidad_stock) {
                printf("No hay suficiente stock. Solo hay %d unidades disponibles.\n", cantidad_stock);
            } else if (cantidad <= 0) {
                printf("La cantidad a vender debe ser positiva.\n");
            } else {
                cantidad_stock -= cantidad;
                ganancias += cantidad * precio_unitario;
                total_ganancias += ganancias;
                printf("Venta completada. Ganancia de esta venta: %.2f\n", ganancias);
            }
        }

        if (opcion == 3) {
            if (!producto_registrado) {
                printf("No hay productos registrados. Agregue un producto primero.\n");
                continue;
            }

            printf("Ingrese la cantidad de producto a reabastecer: ");
            scanf("%d", &cantidad);

            if (cantidad <= 0) {
                printf("La cantidad de reabastecimiento debe ser positiva.\n");
            } else {
                cantidad_stock += cantidad;
                gastos += cantidad * precio_unitario;
                total_gastos += gastos;
                printf("Producto reabastecido. Se ha gastado: %.2f\n", gastos);
            }
        }

        if (opcion == 4) {
            if (!producto_registrado) {
                printf("No hay productos en stock.\n");
                continue;
            }

            printf("\nInformacion del producto:\n");
            printf("ID: %s", id);
            printf("Nombre: %s", nombre);
            printf("Cantidad en stock: %d\n", cantidad_stock);
            printf("Precio unitario: %.2f\n", precio_unitario);
            printf("Ganancia total: %.2f\n", total_ganancias);
        }

        if (opcion == 5) {
            printf("\nGanancias y gastos:\n");
            printf("Ganancias acumuladas: %.2f\n", total_ganancias);
            printf("Gastos acumulados en reabastecimiento: %.2f\n", total_gastos);
        }

        if (opcion == 6) {
            printf("Saliendo del programa...\n");
        }

    } while (opcion != 6);

    return 0;
}
