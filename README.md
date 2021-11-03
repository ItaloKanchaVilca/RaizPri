# Álgebra-Abstracta-Italo-Kancha-Vilca
Laboratorio 4

**NOMBRE:** Italo kancha vilca

**grupo:** Ccomp 3-1


 1.- Implementar un programa que permita calcular su raíz primitiva más pequeña:
 
 - ¿Cual es la raíz primitiva más pequeña de 100049?
 
![image](https://user-images.githubusercontent.com/54363893/139969666-19e20da6-261c-4567-8ee3-2295db46d408.png)

EXPLICACIÓN DEL CODIGO CON COMENTARIOS:

```c ++
#include<bits/stdc++.h>
#include <iostream> 
using namespace std;

// Devuelve verdadera si n es primo
bool esPrimo(int n)
{
    if (n <= 1)  return false;
    if (n <= 3)  return true;

    if (n % 2 == 0 || n % 3 == 0) return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

/* Función iterativa para calcular (x^n)%p en O(logy) */
int potencia(int x, unsigned int y, int p)
{
    int res = 1;     // Inicializar resultado

    x = x % p; // Actualizar x si es mayor o igual que p

    while (y > 0)
    {
        // Si y es impar, multiplica x con el resultado
        if (y & 1)
            res = (res * x) % p;

        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Función para almacenar factores primos de un número
void encontrarFactoresPrimos(unordered_set<int>& s, int n)
{
    // Imprime el número de 2 que dividen n
    while (n % 2 == 0)
    {
        s.insert(2);
        n = n / 2;
    }

    for (int i = 3; i <= sqrt(n); i = i + 2)
    {
        // Mientras i divide n, imprime i y divide n
        while (n % i == 0)
        {
            s.insert(i);
            n = n / i;
        }
    }

    // Esta condición es para manejar el caso cuando n es un número primo mayor que 2
    if (n > 2)
        s.insert(n);
}

// Función para encontrar la raíz primitiva más pequeña de n
int encontrarPrimitivo(int n)
{
    unordered_set<int> s;
    // Comprueba si n es primo o no
    if (isPrime(n) == false)
        return -1;

    // Encuentra el valor de la función Euler de n Dado que n es un número primo, el valor de la función Euler es n-1 ya que hay n-1 números primos relativos.
    int phi = n - 1;

    encontrarFactoresPrimos(s, phi);

    // Comprueba todos los números del 2 al phi

    for (int r = 2; r <= phi; r++)
    {
        // Itera todos los factores primos de phi y verifique si encontramos una potencia con valor 1
        bool flag = false;
        for (auto it = s.begin(); it != s.end(); it++)
        {

            // Verificar si r^((phi)/factoresPrimos) mod n
            // es 1 o no
            if (power(r, phi / (*it), n) == 1)
            {
                flag = true;
                break;
            }
        }

        if (flag == false)
            return r;
    }

    // Si no se encuentra una raíz primitiva
    return -1;
}

int main()
{
    int n = 100049;
    cout << " La raiz primitiva más pequeña de " << n
        << " es " << encontrarPrimitivo(n);
    return 0;
}
```

Ejemplo en Consola:

![Demostración](https://user-images.githubusercontent.com/54363893/135954867-b13f7c5b-2401-4c3d-a287-f76ce19383ff.PNG)
