# 🍲 CARAVAN KITCHEN — Game Design Document (GDD)
**Versión:** 0.1 — MVP Pre-producción  
**Motor:** Unity 2022+ (2D URP)  
**Plataforma objetivo:** Android (Google Play Store)  
**Tipo:** 2D Side-Scrolling Cozy Mobile Game  
**Género:** Exploración / Captura / Cocina / Gestión  
**Estado:** Concepto → MVP

---

## 📋 ÍNDICE

1. [Visión del Juego](#1-visión-del-juego)
2. [Pilares de Diseño](#2-pilares-de-diseño)
3. [Core Loop](#3-core-loop)
4. [Personajes](#4-personajes)
5. [Mapa y Regiones](#5-mapa-y-regiones)
6. [Sistema de Exploración y Captura](#6-sistema-de-exploración-y-captura)
7. [Criaturas Culinarias](#7-criaturas-culinarias)
8. [Ingredientes Recolectables](#8-ingredientes-recolectables)
9. [Sistema de Cocina](#9-sistema-de-cocina)
10. [Recetario](#10-recetario)
11. [Sistema de Pedidos y Venta](#11-sistema-de-pedidos-y-venta)
12. [Economía](#12-economía)
13. [Mejoras de Caravana](#13-mejoras-de-caravana)
14. [Progresión del Jugador](#14-progresión-del-jugador)
15. [UI y UX](#15-ui-y-ux)
16. [Monetización](#16-monetización)
17. [Retención y Live Ops](#17-retención-y-live-ops)
18. [Tono Visual y Arte](#18-tono-visual-y-arte)
19. [Audio](#19-audio)
20. [Roadmap MVP](#20-roadmap-mvp)
21. [Estructura de Proyecto Unity](#21-estructura-de-proyecto-unity)

---

## 1. Visión del Juego

**Caravan Kitchen** es un juego móvil 2D cozy de exploración culinaria, donde el jugador controla a un chef-explorador nómada que viaja por regiones flotantes cubiertas de bruma para capturar criaturas culinarias mágicas y recolectar ingredientes raros. Todo lo recolectado se transforma en platillos dentro de una cocina-caravana ambulante, que el jugador vende, mejora y expande para desbloquear nuevas rutas y recetas.

### Propuesta de valor

> *"Explora la bruma, captura ingredientes vivos, cocina recetas mágicas y expande tu cocina viajera."*

### Referentes

| Juego | Qué toma Caravan Kitchen |
|---|---|
| Zombie Catchers | Loop de captura → proceso → venta → mejora → expansión |
| Stardew Valley | Sensación de progreso diario, colección, pedidos |
| Spiritfarer | Fantasía de caravana / hogar en movimiento |
| Noodle Soup games | Estética cozy, ingredientes vivos, personajes adorables |

---

## 2. Pilares de Diseño

### Pilar 1 — Explorar tiene propósito
Cada salida responde una pregunta: "¿Qué me falta para cocinar lo siguiente?"  
El jugador siempre sale con una meta clara: una criatura, un ingrediente, una receta.

### Pilar 2 — Cocinar es el corazón
La cocina no es solo un menú. Es el sistema que conecta la captura con la venta.  
Cada receta nueva es un descubrimiento que el jugador quiere compartir o completar.

### Pilar 3 — La caravana crece contigo
El hub visible evoluciona con cada mejora: más estaciones, más color, más vida.  
Eso convierte el progreso en algo tangible, no solo en estadísticas.

### Pilar 4 — Loop corto, satisfacción grande
Una sesión de 3–8 minutos debe siempre dar al menos UNA recompensa sentida.  
El jugador debe salir pensando: "Solo una salida más."

### Pilar 5 — Sin presión, con motivación
La monetización y los sistemas de tiempo no deben interrumpir el flow.  
Todo lo premium es opcional y visible. Nunca puertas invisibles.

---

## 3. Core Loop

```
┌─────────────────────────────────────────────────────────────┐
│                     CARAVAN KITCHEN LOOP                    │
│                                                             │
│  1. Revisar pedidos activos y recetas incompletas           │
│         ↓                                                   │
│  2. Elegir región de exploración                            │
│         ↓                                                   │
│  3. Explorar mapa → recolectar ingredientes                 │
│         ↓                                                   │
│  4. Detectar y capturar criaturas culinarias                │
│         ↓                                                   │
│  5. Regresar a la Caravana                                  │
│         ↓                                                   │
│  6. Cocinar recetas con recursos obtenidos                  │
│         ↓                                                   │
│  7. Vender platillos y entregar pedidos                     │
│         ↓                                                   │
│  8. Cobrar monedas + fama culinaria                         │
│         ↓                                                   │
│  9. Mejorar caravana / herramientas / desbloquear región    │
│         ↓                                                   │
│  → Volver al paso 1 (nueva motivación)                     │
└─────────────────────────────────────────────────────────────┘
```

### Micro-loop (por sesión)
- Duración: 3 a 8 minutos
- Sensación: curiosidad → descubrimiento → satisfacción → anticipación

### Macro-loop (por semana)
- Mejorar caravana, desbloquear zona, completar recetario, llenar bestiario

---

## 4. Personajes

### 4.1 Protagonista — KIRI

| Atributo | Descripción |
|---|---|
| Nombre | Kiri |
| Rol | Chef explorador nómada |
| Silueta | Redonda, amigable, tierna |
| Estatura | Media-baja, compacta |
| Paleta | Crema, turquesa, ámbar miel |

**Equipamiento visual:**
- Sombrero de cocina remendado con goggles plegados
- Mochila-caldero con tapa
- Bufanda larga que anima al correr
- Red plegable al costado
- Guantes y botas de campo

**Animaciones base (Unity Animator):**
- `Idle` — respira, mueve bufanda
- `Walk` — paso lateral 2D
- `Run` — variante rápida
- `Jump` — salto suave
- `Collect` — agacharse y tomar
- `ThrowNet` — lanzar red
- `PlaceBait` — agacharse y dejar cebo
- `Cook` — revolver en caldero
- `Celebrate` — salto con brazos arriba
- `Tired` — caminar despacio si mochila llena

---

### 4.2 Compañero — FUMI

| Atributo | Descripción |
|---|---|
| Nombre | Fumi |
| Apariencia | Nubecita pequeña con ojos brillantes |
| Función jugable | Detecta rarezas, señala rutas ocultas, guía tutoriales |
| Función emocional | Comentarios de recetas, reacciones a capturas |

**Comportamientos:**
- Brilla cuando hay criatura rara cercana
- Flota más alto cuando hay ingrediente especial
- Reacciona expresivamente al cocinar recetas nuevas

---

### 4.3 NPCs de Mercado

| NPC | Rol |
|---|---|
| Marchante Brulo | Pedidos normales diarios |
| Señora Velta | Pedidos especiales de recetas raras |
| El Anciano Nomo | Recetas legendarias y pistas de zonas |
| Kofi el Trotamundos | Ingredientes inusuales a cambio de platillos |

---

## 5. Mapa y Regiones

### Estructura del mundo

```
              [ MERCADO SUSPENDIDO ]
                      ↑
      ┌───────────────┤───────────────┐
      ↑               ↑               ↑
[ Arrecife      [ Bosque de       [ Barranco
 de Nubes ]      Vapor Dulce ]    del Caldero ]
      ↑               ↑               ↑
      └───────────────┤───────────────┘
                      ↑
            [ PRADERA DE BRUMA ]  ← Zona inicial
                      ↑
              [ CARAVANA CELESTE ]  ← Hub base
```

---

### 5.1 Caravana Celeste (Hub principal)

**Función:** Base de operaciones del jugador.  
**Aquí puedes:**
- Cocinar en estaciones disponibles
- Ver y aceptar pedidos activos
- Mejorar herramientas y estaciones
- Decorar y ampliar la caravana
- Revisar recetario y bestiario
- Viajar a regiones

**Evolución visual:**
| Nivel de caravana | Cambios visibles |
|---|---|
| 1 | Caldero básico, toldo pequeño, espacio mínimo |
| 2 | Parrilla añadida, toldo más grande |
| 3 | Mesa dulce, farolitos, más espacio |
| 4 | Secador, molino, decoraciones, mascota de tienda |
| 5 | Estación completa, clientes simultáneos, apariencia de restaurante viajero |

---

### 5.2 Pradera de Bruma (Zona 1 — Tutorial)

| Atributo | Detalle |
|---|---|
| Ambiente | Prados flotantes suaves, niebla baja, luz dorada |
| Dificultad | ★☆☆☆☆ |
| Ingredientes | Baya de bruma, Hoja picante, Seta blanda, Raíz dulce |
| Criaturas | Puffshroom, Mielín, Raicita Viva |
| Rareza especial | Puffshroom Dorado (solo amanecer) |
| Desbloqueo | Disponible desde inicio |

**Mecánicas introducidas:** recolectar, lanzar red, colocar cebo básico

---

### 5.3 Bosque de Vapor Dulce (Zona 2)

| Atributo | Detalle |
|---|---|
| Ambiente | Árboles con vapor cálido, flores brillantes, charcos de calor |
| Dificultad | ★★☆☆☆ |
| Ingredientes | Flor mielada, Polen luminoso, Néctar espeso, Musgo dulce |
| Criaturas | Mielín Mayor, Broteín, Oruga Caramelizada |
| Rareza especial | Avispa Ambarino (solo días de lluvia) |
| Desbloqueo | Mejora de Red nivel 2 + 500 monedas |

**Mecánicas introducidas:** cebo aromático, trampa de calor

---

### 5.4 Arrecife de Nubes (Zona 3)

| Atributo | Detalle |
|---|---|
| Ambiente | Plataformas aéreas, corrientes de aire, cielo azul profundo |
| Dificultad | ★★★☆☆ |
| Ingredientes | Alga celeste, Sal de nube, Escama de aire |
| Criaturas | Nubipez, Almeja Flotante, Caracol de Canela |
| Rareza especial | Nubipez Iridiscente (clima despejado) |
| Desbloqueo | Mejora de Mochila nivel 2 + 1200 monedas |

**Mecánicas introducidas:** campana de llamada, movimiento vertical

---

### 5.5 Barranco del Caldero (Zona 4)

| Atributo | Detalle |
|---|---|
| Ambiente | Grietas minerales, vapor sulfuroso suave, tono ámbar/naranja |
| Dificultad | ★★★★☆ |
| Ingredientes | Cristal de caldo, Sal mineral, Especia volcánica |
| Criaturas | Salamandra de Azafrán, Topo Especiado, Crisálida Ardiente |
| Rareza especial | Salamandra Rubí (solo de noche) |
| Desbloqueo | Herramienta de Captura nivel 3 + 2500 monedas |

**Mecánicas introducidas:** frasco termoresistente, trampa de vapor frío

---

### 5.6 Mercado Suspendido (Zona social — Hub económico)

| Atributo | Detalle |
|---|---|
| Ambiente | Mercado flotante colorido, faroles, múltiples puestos |
| Función | NPCs, pedidos especiales, recetas legendarias, mejoras únicas |
| Desbloqueo | Completar pedido especial de Zona 2 + 800 fama culinaria |

**Aquí NO cazas**. Aquí vendes, intercambias, descubres y recibes encargos de alto valor.

---

## 6. Sistema de Exploración y Captura

### 6.1 Movimiento en mapa

- 2D lateral (side-scrolling)
- Caminar, correr, saltar
- Interactuar con plantas y objetos del entorno
- Detectar criaturas por indicador de Fumi (brillo)

### 6.2 Herramientas de captura

| Herramienta | Tipo | Uso | Criaturas objetivo |
|---|---|---|---|
| Red básica | Lanzar | Criaturas lentas en suelo | Puffshroom, Raicita |
| Cebo de miel | Colocar | Criaturas atraídas por dulce | Mielín, Broteín |
| Cebo aromático | Colocar | Criaturas curiosas | Oruga, Topo |
| Campana de bruma | Activar | Criaturas voladoras | Nubipez, Almeja flotante |
| Trampa de calor | Colocar | Criaturas de vapor | Salamandra, Crisálida |
| Frasco termoresistente | Lanzar | Criaturas ardientes | Salamandra Rubí |

### 6.3 Comportamiento de criaturas

| Comportamiento | Descripción |
|---|---|
| `IDLE` | La criatura deambula en zona definida |
| `ALERT` | Detectó al jugador, se pone nerviosa |
| `FLEE` | Huye si el jugador se acerca demasiado |
| `ATTRACTED` | Va hacia el cebo |
| `CAPTURED` | Animación de captura, ingresa al inventario |
| `RARE_SPAWN` | Solo aparece bajo condición especial |

### 6.4 Condiciones especiales de aparición

| Condición | Criaturas afectadas |
|---|---|
| Amanecer (06:00–08:00 in-game) | Puffshroom Dorado, Nubipez Iridiscente |
| Lluvia | Avispa Ambarino, Broteín |
| Noche (20:00–00:00 in-game) | Salamandra Rubí, Caracol de Canela |
| Clima despejado | Almeja Flotante, Crisálida Ardiente |

> ⏱ El tiempo in-game puede configurarse como ciclo de 24 minutos reales = 1 día completo, o adaptarse a 4 fases fijas por sesión.

---

## 7. Criaturas Culinarias

### Tabla de criaturas base

| ID | Nombre | Zona | Rareza | Lo que aporta | Herramienta |
|---|---|---|---|---|---|
| C01 | Puffshroom | Pradera | Común | Esencia de hongo | Red básica |
| C02 | Mielín | Pradera | Común | Néctar puro | Cebo de miel |
| C03 | Raicita Viva | Pradera | Común | Raíz fresca | Red básica |
| C04 | Puffshroom Dorado | Pradera | Raro | Esencia dorada | Red básica + amanecer |
| C05 | Mielín Mayor | Bosque | Poco común | Néctar espeso | Cebo de miel |
| C06 | Broteín | Bosque | Poco común | Brote cristalino | Cebo aromático |
| C07 | Oruga Caramelizada | Bosque | Poco común | Seda dulce | Cebo aromático |
| C08 | Avispa Ambarino | Bosque | Raro | Polen áureo | Trampa especial + lluvia |
| C09 | Nubipez | Arrecife | Poco común | Escama celeste | Campana |
| C10 | Almeja Flotante | Arrecife | Poco común | Perla salina | Campana |
| C11 | Caracol de Canela | Arrecife | Raro | Concha especiada | Red + noche |
| C12 | Nubipez Iridiscente | Arrecife | Muy raro | Escama prisma | Campana + clima |
| C13 | Salamandra de Azafrán | Barranco | Poco común | Piel azafrán | Frasco termoresistente |
| C14 | Topo Especiado | Barranco | Poco común | Polvo especiado | Trampa de vapor |
| C15 | Crisálida Ardiente | Barranco | Raro | Seda de fuego | Trampa de vapor frío |
| C16 | Salamandra Rubí | Barranco | Muy raro | Esencia rubí | Frasco termoresistente + noche |

---

## 8. Ingredientes Recolectables

### Tabla de ingredientes base

| ID | Nombre | Zona | Rareza | Uso principal |
|---|---|---|---|---|
| I01 | Baya de bruma | Pradera | Común | Sopas, tés, jaleas |
| I02 | Hoja picante | Pradera | Común | Guisos, brochetas |
| I03 | Seta blanda | Pradera | Común | Sopas, guisos |
| I04 | Raíz dulce | Pradera | Común | Dulces, tés |
| I05 | Flor mielada | Bosque | Poco común | Tés, postres |
| I06 | Polen luminoso | Bosque | Poco común | Recetas brillantes |
| I07 | Néctar espeso | Bosque | Poco común | Jaleas, postres |
| I08 | Musgo dulce | Bosque | Poco común | Caldos, sopas |
| I09 | Alga celeste | Arrecife | Poco común | Sopas, guisos marinos |
| I10 | Sal de nube | Arrecife | Poco común | Sazonar, conservas |
| I11 | Escama de aire | Arrecife | Raro | Recetas aéreas |
| I12 | Cristal de caldo | Barranco | Poco común | Caldos concentrados |
| I13 | Sal mineral | Barranco | Común | Sazonar, conservas |
| I14 | Especia volcánica | Barranco | Raro | Recetas ardientes |

---

## 9. Sistema de Cocina

### 9.1 Estaciones de cocina

| ID | Estación | Desbloqueo | Recetas |
|---|---|---|---|
| E01 | Caldero | Inicio | Sopas, caldos, infusiones |
| E02 | Parrilla de piedra | Caravana nivel 2 | Brochetas, asados |
| E03 | Mesa dulce | Caravana nivel 3 | Jaleas, postres, dulces |
| E04 | Secador de vapor | Caravana nivel 3 | Hierbas secas, hongos, especias |
| E05 | Molino celeste | Caravana nivel 4 | Harinas, polvos especiales |

### 9.2 Mecánica de cocina

Cada receta requiere:
- 1–3 ingredientes + opcionalmente 1 criatura/esencia
- Ser preparada en la estación correcta
- Un tiempo de cocción (en tiempo real: 30 seg – 3 min, acelerado con rewarded ad)

Resultado:
- Un platillo con nombre, ilustración y descripción
- Valor de venta base
- Posible uso para pedido especial

### 9.3 Calidad de platillo

Dependiendo del estado de los ingredientes, el platillo puede salir en 3 calidades:

| Calidad | Condición | Multiplicador de precio |
|---|---|---|
| ⭐ Normal | Ingredientes básicos | x1.0 |
| ⭐⭐ Especial | Ingrediente raro incluido | x1.5 |
| ⭐⭐⭐ Legendario | Criatura rara + ingrediente especial | x2.5 |

---

## 10. Recetario

### Recetas iniciales (MVP)

| ID | Receta | Estación | Ingredientes | Criatura | Calidad |
|---|---|---|---|---|---|
| R01 | Sopa de Bruma | Caldero | Baya de bruma, Seta blanda | — | Normal |
| R02 | Caldo de Hoja | Caldero | Hoja picante, Raíz dulce | — | Normal |
| R03 | Brocheta de Raicita | Parrilla | Hoja picante | Raicita Viva | Especial |
| R04 | Té de Rocío | Caldero | Flor mielada, Raíz dulce | — | Normal |
| R05 | Guiso de Puffshroom | Caldero | Seta blanda, Musgo dulce | Puffshroom | Especial |
| R06 | Jalea de Baya Nublada | Mesa dulce | Baya de bruma, Néctar espeso | — | Normal |
| R07 | Pastelillo de Mielín | Mesa dulce | Flor mielada, Polen luminoso | Mielín | Especial |
| R08 | Caldo Celeste | Caldero | Alga celeste, Sal de nube | — | Normal |
| R09 | Seta Dulce Asada | Parrilla | Seta blanda, Raíz dulce | — | Normal |
| R10 | Néctar Espumoso | Mesa dulce | Néctar espeso, Baya de bruma | Mielín Mayor | Legendario |
| R11 | Brocheta de Nubipez | Parrilla | Sal de nube, Especia volcánica | Nubipez | Especial |
| R12 | Conserva de Canela | Secador | Sal mineral, Musgo dulce | Caracol de Canela | Especial |

### Categorías de recetas

- **Comunes** — fáciles, venta diaria
- **Raras** — requieren criatura específica
- **De temporada** — solo en ciertas condiciones del día
- **Legendarias** — requieren rareza + ingrediente especial
- **Encargo** — pedida por NPC específico

---

## 11. Sistema de Pedidos y Venta

### Tipos de pedido

| Tipo | Frecuencia | Recompensa | Expiración |
|---|---|---|---|
| Pedido normal | Siempre disponible | Monedas base | 24 horas in-game |
| Pedido especial | 2–3 por día | Monedas + fama | 48 horas in-game |
| Pedido raro | 1 por semana | Mejoras únicas | 72 horas in-game |
| Pedido de evento | Temporal | Recompensas exclusivas | Duración del evento |

### Flujo de venta

```
Jugador cocina platillo
       ↓
Ingresa al inventario de platillos
       ↓
Jugador puede:
  A) Vender directamente (precio base)
  B) Entregar pedido específico (precio + bonus)
  C) Guardar para pedido raro futuro
```

### Clientes espontáneos

En la caravana aparecen clientes aleatorios que pagan entre 10–30% más si les das su platillo favorito.  
Sistema ligero: cada cliente tiene 1–2 platillos preferidos visibles en su burbuja.

---

## 12. Economía

### Monedas del juego

| Moneda | Obtención | Uso |
|---|---|---|
| 🪙 Monedas de Bruma | Ventas, pedidos, misiones | Mejoras normales, herramientas, acceso a zonas |
| ⭐ Fama Culinaria | Pedidos especiales, recetas nuevas, eventos | Desbloqueo de NPCs, recetas legendarias, mejoras únicas |
| 💎 Cristales (premium) | IAP, muy ocasionalmente free | Cosméticos, skins, aceleraciones opcionales |

### Valores de venta base

| Calidad | Rango de precio |
|---|---|
| Normal | 20–60 monedas |
| Especial | 80–150 monedas |
| Legendario | 200–400 monedas |

### Costos de mejora base

| Mejora | Costo |
|---|---|
| Red nivel 2 | 500 monedas |
| Mochila nivel 2 | 400 monedas |
| Parrilla | 700 monedas |
| Acceso a Zona 2 | 500 monedas |
| Acceso a Zona 3 | 1,200 monedas |
| Acceso a Zona 4 | 2,500 monedas |

---

## 13. Mejoras de Caravana

### 13.1 Herramientas de captura

| Mejora | Nivel | Efecto | Costo |
|---|---|---|---|
| Red | 1 → 2 → 3 | Mayor alcance, criaturas más rápidas | 300 / 800 / 1500 |
| Cebo | 1 → 2 → 3 | Mayor duración, atrae más criaturas | 200 / 600 / 1200 |
| Campana | 1 → 2 | Rango de llamada, criaturas voladoras raras | 400 / 1000 |
| Frasco térmico | 1 → 2 | Aguanta más criaturas ardientes | 600 / 1400 |

### 13.2 Capacidad

| Mejora | Efecto |
|---|---|
| Mochila nivel 2 | +4 espacios de ingredientes |
| Mochila nivel 3 | +4 espacios + espacio criatura especial |
| Caja de ingredientes | +8 espacios en caravana |

### 13.3 Estaciones de cocina

Ver tabla en sección 9.1.

### 13.4 Caravana (visual y funcional)

| Nivel | Requisito | Mejora visual | Mejora funcional |
|---|---|---|---|
| 1 | Inicio | Caldero, toldo pequeño | 1 platillo simultáneo |
| 2 | 800 monedas + 3 pedidos | Parrilla añadida | 2 platillos simultáneos |
| 3 | 1500 monedas + 8 pedidos | Mesa dulce, farolitos | 3 platillos + clientes espontáneos |
| 4 | 3000 monedas + 150 fama | Secador, molino, decoración | 4 platillos + pedido raro disponible |
| 5 | 5000 monedas + 400 fama | Estación completa, aspecto restaurante | Clientes simultáneos, eventos |

---

## 14. Progresión del Jugador

### 4 capas de progresión

```
INMEDIATA (segundos/minutos)
  └─ Capturar criatura, recolectar ingrediente, cocinar receta, entregar pedido

DIARIA (por sesión)
  └─ Completar 3 pedidos normales, misión del día, ingrediente especial del día

COLECCIÓN (días/semanas)
  └─ Completar recetario, completar bestiario, desbloquear todas las recetas de una zona

ESTRUCTURAL (semanas/meses)
  └─ Mejorar caravana al máximo, desbloquear todas las zonas, completar temporada culinaria
```

### Curva de progreso MVP

| Sesión | Meta | Desbloqueo |
|---|---|---|
| 1 | Tutorial + 1ª venta | Red básica, Caldero |
| 2–3 | Completar 5 recetas comunes | Cebo de miel, Mesa dulce |
| 4–6 | Llenar bestiario zona 1 | Caravana nivel 2, acceso zona 2 |
| 7–10 | Primer pedido especial | Parrilla, Campana nivel 1 |
| 11–15 | Acceso zona 3 | Mochila nivel 2, recetas raras |
| 16–20 | Primera receta legendaria | Caravana nivel 3, Mercado Suspendido |

---

## 15. UI y UX

### Pantallas principales

| Pantalla | Contenido |
|---|---|
| Mapa Mundial | Zonas disponibles, costos de acceso, región actual |
| Exploración | Personaje en mapa, inventario rápido, herramientas |
| Caravana (Hub) | Estaciones, botón de pedidos, botón de mejoras |
| Recetario | Recetas descubiertas / bloqueadas, ingredientes faltantes |
| Bestiario | Criaturas vistas / capturadas, rareza, horario |
| Pedidos | Lista activa, recompensas, temporizadores |
| Mejoras | Árbol visual de upgrades por categoría |
| Tienda | IAP, cosméticos, moneda premium |

### Principios de UX

- Pantalla de exploración: HUD mínimo, máximo espacio de juego
- Inventario visible con burbuja rápida (sin abrir menú)
- Recetas incompletas siempre visibles desde la caravana
- Notificación de pedido vencido: suave, sin interrumpir
- Animaciones de feedback claras: captura exitosa, cocina terminada, venta realizada

---

## 16. Monetización

### Modelo base
**Freemium con rewarded ads opcionales + IAP cosmético**

No hay paywall que bloquee la progresión central.  
No hay anuncios interstitiales forzados después de expedición.

### Rewarded Ads (opcionales)

| Activador | Recompensa |
|---|---|
| Ver ad voluntario en venta | Duplicar ganancia de ese platillo |
| Ver ad en cocina | Terminar cocción al instante |
| Ver ad en expedición | Aparecer criatura rara por 30 segundos |
| Ver ad en mochila llena | +2 espacios temporales para esa salida |
| Ver ad al volver sin captura | Reintentar con cebo premium gratis |

**Límite recomendado:** máximo 5 rewarded ads por sesión de juego de 30 min.

### IAP (Compras en app)

| Producto | Precio aprox. | Qué incluye |
|---|---|---|
| Quitar anuncios | $1.99 USD | Sin ads opcionales forzados (los rewarded siguen opcionales) |
| Pack Inicial del Chef | $2.99 USD | Skin de Kiri + 500 monedas + 3 cristales |
| Skin de Caravana — Nocturna | $1.99 USD | Rediseño visual de la caravana |
| Skin de Caravana — Festiva | $1.99 USD | Tema de temporada |
| Bolsa de Cristales (100) | $0.99 USD | Moneda premium |
| Pase de Temporada Culinaria | $4.99 USD | Recetas exclusivas, skin, bonus de fama |

---

## 17. Retención y Live Ops

### Sistema diario (sin timer agresivo)

- ✅ Misión del día: "Captura 3 Puffshrooms"
- ✅ Pedido especial rotativo de NPC
- ✅ Ingrediente especial disponible hoy
- ✅ Criatura brillante del día (rareza aumentada)

### Sistema semanal

- 🍳 Receta semanal: nueva receta descubrible solo esta semana
- 🗺️ Ruta limitada: zona alternativa temporal con recursos especiales

### Eventos de temporada

- Temporada de Lluvia → criaturas y recetas acuáticas
- Festival de Fuego → Barranco con criaturas únicas, pedidos de alta fama
- Feria del Mercado → Pedidos premium masivos, ingredientes intercambiables

---

## 18. Tono Visual y Arte

### Paleta principal

| Rol | Color | Uso |
|---|---|---|
| Fondo base | #F5F0E8 (crema) | Cielos, bruma baja |
| Acento turquesa | #4DB6AC | UI, botones, Fumi |
| Ámbar miel | #FFB347 | Criaturas, caldero, accents |
| Verde salvia | #87A878 | Vegetación, decoración |
| Rosa baya | #E08080 | Recetas dulces, flores |
| Gris neblina | #B0B8C1 | Bruma, sombras suaves |

### Estilo de arte

- 2D ilustrado, líneas suaves, sombras simples
- Sin pixel art (para mayor expresividad y lectura en móvil)
- Criaturas: aspecto "comestible adorable" sin violencia visual
- Fondos: capas de paralaje suave para profundidad
- UI: iconos claros, tipografía redondeada, sin serif agresivo

### Resolución base

- 1080 × 1920 (portrait)
- UI escalada para 720p y 1440p
- Sprites: mínimo 2x para pantallas retina

---

## 19. Audio

### Música

| Escena | Estilo | Tempo |
|---|---|---|
| Caravana (Hub) | Cozy jazz ligero, ukelele + marimba | Lento |
| Pradera de Bruma | Folk suave, flauta y acordeón | Moderado |
| Bosque de Vapor | Ambient cálido, cuerdas | Lento |
| Arrecife de Nubes | Viento suave, arpa | Lento |
| Barranco del Caldero | Percusión suave, resonadores | Moderado |
| Mercado Suspendido | Jazz animado, múltiples instrumentos | Animado |

### SFX clave

- Captura exitosa: "plop" satisfactorio
- Cocinando: burbujeo + chisporroteo
- Venta realizada: campanita + monedas
- Ingrediente recolectado: sonido suave de pop
- Fumi reacciona: suave "mhm" o destello sonoro
- Criatura rara: jingle corto especial

---

## 20. Roadmap MVP

### Fase 0 — Fundación (2 semanas)
- [ ] Proyecto Unity creado (2D URP, Android Build Support)
- [ ] Estructura de carpetas base
- [ ] Personaje Kiri: sprite + animaciones base (Idle, Walk, Jump)
- [ ] Cámara 2D con seguimiento suave
- [ ] Movimiento horizontal + salto

### Fase 1 — Exploración básica (2 semanas)
- [ ] Mapa Pradera de Bruma: plataformas, fondo con paralaje
- [ ] Sistema de recolección (I01–I04)
- [ ] Inventario simple (ScriptableObject por ingrediente)
- [ ] 1 criatura IA: Puffshroom (idle + flee + captured)

### Fase 2 — Captura (2 semanas)
- [ ] Herramienta Red básica: animación + colisión + resultado
- [ ] Cebo de miel: colocar, timer, atracción de Mielín
- [ ] Feedback visual de captura exitosa
- [ ] Compañero Fumi: brillo al detectar rareza

### Fase 3 — Caravana y Cocina (3 semanas)
- [ ] Hub Caravana: escena y navegación
- [ ] Caldero: animación + timer de cocción
- [ ] ScriptableObject por Receta (ingredientes, tiempo, resultado)
- [ ] Inventario de platillos
- [ ] 5 recetas funcionales (R01–R05)

### Fase 4 — Pedidos y Economía (2 semanas)
- [ ] Sistema de pedidos: 3 pedidos activos, timer, recompensa
- [ ] Monedas: obtener, mostrar, gastar
- [ ] 2 NPCs básicos con pedidos
- [ ] UI de venta rápida

### Fase 5 — Mejoras (1 semana)
- [ ] 4 mejoras de herramienta funcionales
- [ ] Caravana nivel 2 desbloqueada con monedas
- [ ] Parrilla habilitada

### Fase 6 — Pulido MVP (2 semanas)
- [ ] SFX básicos
- [ ] Música de fondo (loop)
- [ ] UI limpia y legible
- [ ] Tutorial básico (Fumi guía)
- [ ] 1 rewarded ad opcional (duplicar venta)
- [ ] Build Android → prueba interna Google Play

**Total estimado: ~14 semanas para MVP jugable**

---

## 21. Estructura de Proyecto Unity

```
Assets/
├── _Scripts/
│   ├── Player/
│   │   ├── PlayerController.cs
│   │   ├── PlayerAnimator.cs
│   │   └── PlayerInventory.cs
│   ├── Creatures/
│   │   ├── CreatureBase.cs
│   │   ├── CreatureAI.cs
│   │   └── CreatureData.cs          ← ScriptableObject
│   ├── Ingredients/
│   │   ├── IngredientData.cs         ← ScriptableObject
│   │   └── IngredientSpawner.cs
│   ├── Cooking/
│   │   ├── CookingStation.cs
│   │   ├── RecipeData.cs             ← ScriptableObject
│   │   └── RecipeBook.cs
│   ├── Orders/
│   │   ├── OrderData.cs              ← ScriptableObject
│   │   ├── OrderManager.cs
│   │   └── OrderUI.cs
│   ├── Economy/
│   │   ├── CurrencyManager.cs
│   │   └── UpgradeData.cs            ← ScriptableObject
│   ├── Map/
│   │   ├── RegionData.cs             ← ScriptableObject
│   │   └── WorldMapManager.cs
│   ├── Companion/
│   │   └── FumiController.cs
│   ├── UI/
│   │   ├── HUDController.cs
│   │   ├── InventoryUI.cs
│   │   ├── RecipeBookUI.cs
│   │   └── BestiaryUI.cs
│   └── Managers/
│       ├── GameManager.cs
│       ├── SaveManager.cs
│       └── AudioManager.cs
│
├── _Data/                            ← Todos los ScriptableObjects
│   ├── Creatures/
│   ├── Ingredients/
│   ├── Recipes/
│   ├── Orders/
│   ├── Upgrades/
│   └── Regions/
│
├── Art/
│   ├── Characters/
│   │   ├── Kiri/
│   │   └── Fumi/
│   ├── Creatures/
│   ├── Backgrounds/
│   ├── UI/
│   └── VFX/
│
├── Audio/
│   ├── Music/
│   └── SFX/
│
├── Prefabs/
│   ├── Player/
│   ├── Creatures/
│   ├── Ingredients/
│   └── UI/
│
├── Scenes/
│   ├── MainMenu.unity
│   ├── Caravan.unity
│   ├── Region_Pradera.unity
│   ├── Region_Bosque.unity
│   ├── Region_Arrecife.unity
│   ├── Region_Barranco.unity
│   └── Mercado.unity
│
└── Plugins/
    └── (AdMob SDK, etc.)
```

---

## 📌 Notas de producción

- Toda la data del juego (criaturas, recetas, ingredientes) debe vivir en **ScriptableObjects**, no hardcodeada en scripts.
- Usar **Addressables** para cargar escenas por región y evitar tiempos de carga altos en móvil.
- **SaveManager** debe usar `Application.persistentDataPath` con JSON, nunca PlayerPrefs para datos importantes.
- Los rewarded ads solo inicializarlos con **Google AdMob SDK** una vez el MVP esté probado.
- Usar **Unity 2D Physics** estándar para el movimiento, no física personalizada en MVP.
- Animaciones de personaje: **Animator Controller** con blend trees para idle/walk/run.

---

*Caravan Kitchen GDD — v0.1 — Confidencial / Uso interno*  
*Revisión: Mayo 2026*
