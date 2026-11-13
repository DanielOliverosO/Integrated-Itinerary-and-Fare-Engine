# Integrated-Itinerary-and-Fare-Engine
## Integrantes

- Daniel Andres Oliveros Olmos
- Segundo integrante cancelo materia
## Cómo compilarlo
```bash
g++ -std=c++17 -Wall -Wextra -o practice main.cpp
./practice
```
## Preguntas de defensa
 
### Pregunta 1: ¿qué pasa si el destructor de `TransportMode` no es virtual?
 
Los modos se guardan en la red como `std::unique_ptr<TransportMode>`, es decir, a través de un puntero a la clase base. Cuando el `unique_ptr` libera el objeto, hace un `delete` sobre ese puntero base.
 
- **Con destructor virtual**, C++ elige el destructor según el tipo real del objeto. Se ejecuta primero el destructor de la clase derivada (por ejemplo `TouristCable`) y después el de la base, de modo que se destruye el objeto completo.
- **Sin destructor virtual**, solo se ejecuta el destructor de la base. Los miembros propios de la clase derivada nunca se destruyen y los recursos que administren se pierden. Según el estándar de C++, esto es comportamiento indefinido.
Por eso `~TransportMode()` está declarado `virtual`. Por la misma razón, `~Passenger()` también lo es.
 
### Pregunta 2
 
El enunciado menciona dos preguntas de defensa, pero la pregunta 2 no se especifica en el documento.
