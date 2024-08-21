# Maquina-Expendedora-en-c-
Maquina expendedora la cual fue creada en c# usando los comandos básicos de c#. 

```
using System;
using System.Collections.Generic;

class VendingMachine
{
    private Dictionary<string, (int price, int stock)> products;

    public VendingMachine()
    {
        products = new Dictionary<string, (int, int)>
        {
            { "A1", (50, 10) }, // Producto A1: Precio 50, Stock 10
            { "B2", (75, 5) },  // Producto B2: Precio 75, Stock 5
            { "C3", (100, 2) }  // Producto C3: Precio 100, Stock 2
        };
    }

    public void DisplayProducts()
    {
        Console.WriteLine("Productos disponibles:");
        foreach (var item in products)
        {
            Console.WriteLine($"Código: {item.Key}, Precio: {item.Value.price} centavos, Stock: {item.Value.stock}");
        }
    }

    public bool PurchaseProduct(string code, int moneyInserted)
    {
        if (!products.ContainsKey(code))
        {
            Console.WriteLine("Código de producto no válido.");
            return false;
        }

        var (price, stock) = products[code];

        if (stock <= 0)
        {
            Console.WriteLine("El producto está agotado.");
            return false;
        }

        if (moneyInserted < price)
        {
            Console.WriteLine("Dinero insuficiente.");
            return false;
        }

        // Actualizar stock y mostrar cambio
        products[code] = (price, stock - 1);
        int change = moneyInserted - price;
        Console.WriteLine($"Compra exitosa. Cambio: {change} centavos.");
        return true;
    }
}

class Program
{
    static void Main()
    {
        VendingMachine vendingMachine = new VendingMachine();

        while (true)
        {
            Console.WriteLine("\n--- Máquina Expendedora ---");
            vendingMachine.DisplayProducts();

            Console.Write("Ingrese el código del producto: ");
            string code = Console.ReadLine();

            Console.Write("Ingrese el dinero insertado en centavos: ");
            if (int.TryParse(Console.ReadLine(), out int moneyInserted))
            {
                vendingMachine.PurchaseProduct(code, moneyInserted);
            }
            else
            {
                Console.WriteLine("Entrada de dinero no válida.");
            }

            Console.Write("¿Desea realizar otra compra? (s/n): ");
            if (Console.ReadLine().ToLower() != "s")
            {
                break;
            }
        }
    }
}

```



![image](https://github.com/user-attachments/assets/fa68181f-326a-4d89-8f64-233a259a09a0)


                                                                                         
