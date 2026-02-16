# GALAGA 3D (Tercera Persona) — Diseño y Mecánicas

Este proyecto recrea la esencia del clásico GALAGA en un entorno 3D accesible desde el navegador usando A-Frame, HTML, CSS y JavaScript.  
El enfoque mantiene la jugabilidad arcade: controles simples, oleadas de enemigos, disparo constante y sistema de puntaje.

---

## Concepto de juego

Shooter espacial 3D en tercera persona (vista desde la espalda) donde el jugador controla una nave que:
- Se mueve solo lateralmente (izquierda/derecha).
- Dispara hacia el frente para destruir enemigos.
- Sobrevive a oleadas con dificultad creciente.
- Acumula puntos y (opcionalmente) obtiene mejoras con power-ups.

---

## Controles

- A: mover izquierda
- D: mover derecha
- Space: disparar
- P o Esc: pausar (opcional)

El movimiento es únicamente en el eje X (lateral).

---

## Cámara (tercera persona)

La cámara se ubica detrás del jugador y sigue estas reglas:
- Sigue al jugador solo en X (con suavizado).
- Mantiene una distancia fija en Z y una altura fija en Y.
- Siempre mira hacia el frente (zona donde aparecen los enemigos).

Esto permite ver modelos 3D y profundidad sin complicar el control.

---

## Movimiento del jugador (solo lateral)

- Movimiento: eje X únicamente.
- Límites del escenario: ejemplo X ∈ [-8, 8] (ajustable).
- Feeling recomendado:
  - Aceleración suave al moverse
  - Frenado suave al soltar teclas
  - Velocidad máxima fija para mantener estilo arcade

---

## Disparo y combate

### Disparo del jugador
- Disparo recto hacia el frente (eje Z).
- Cadencia (cooldown): 200–300 ms.
- Las balas desaparecen si:
  - salen de rango (distancia máxima)
  - chocan con un enemigo

### Enemigos
Los enemigos manejan dos estados principales:
1. Formación
   - Se mueven en grupo con patrón tipo wave (oscilación).
2. Ataque
   - 1–2 enemigos se desprenden y hacen picadas hacia el jugador (curva simple).

### Disparo enemigo (opcional)
- Balas lentas y visibles.
- Frecuencia baja al inicio (sube por nivel).

---

## Colisiones (reglas)

El jugador pierde vida si:
- Choca con un enemigo.
- Recibe un proyectil enemigo.

El enemigo muere si:
- Recibe un proyectil del jugador.

Recomendación técnica: usar hitboxes simples (esfera/caja invisible) en vez de colisión por malla.

---

## Vidas y Game Over

- Vidas iniciales: 3
- Al perder vida:
  - Explosión o efecto visual
  - Invulnerabilidad temporal (aprox. 1 segundo) con parpadeo
- Game Over cuando las vidas llegan a 0

---

## Puntaje (score)

Puntajes sugeridos:
- Enemigo básico: 50
- Enemigo rápido: 100
- Enemigo tanque: 200

Opcional:
- Vida extra cada X puntos (ej. 10,000)
- Bonos por combos

---

## Progresión por oleadas (dificultad)

Cada oleada aumenta la dificultad con:
- Más enemigos por formación
- Mayor velocidad de movimiento
- Mayor frecuencia de ataques en picada
- Mayor frecuencia de disparos enemigos
- Menor tiempo entre oleadas

Ejemplo simple:
- Oleada 1: básicos, 1 atacante
- Oleada 2: básicos + rápidos, 2 atacantes
- Oleada 3: aparece tanque
- Oleada 4: más disparos enemigos
- Oleada 5: mini-boss (opcional)

---

## Tipos de enemigos (mínimos)

1. Básico (1 hit)
   - Formación + ataques ocasionales
2. Rápido (1 hit)
   - Zig-zag corto o movimientos más rápidos
3. Tanque (3 hits)
   - Lento, más resistente, puede disparar más

---

## Power-ups (opcional)

Power-ups simples para mantener el estilo arcade:
- Double Shot (disparo doble por 10 s)
- Rapid Fire (cadencia más rápida por 8–10 s)
- Shield (absorbe 1 golpe)

Probabilidad de drop: 10–20% al destruir enemigos especiales.

---

## Escenario 3D (sensación de profundidad)

Para que se sienta 3D aunque el movimiento sea lateral:
- Sky o skybox con estrellas
- Plano o pista sutil (grid tenue o piso oscuro)
- Efecto de velocidad:
  - partículas de estrellas moviéndose hacia el jugador
  - líneas de luz o túnel espacial

---

## Modelos 3D (Blender)

Modelos recomendados (low poly):
- Nave del jugador
- 3 tipos de naves enemigas (básico, rápido, tanque)
- Bala del jugador / bala enemiga
- Power-up (capsula/cubo)
- Explosión (sprite o partículas)

Formato recomendado: .glb / glTF  
Importante: pivot/origen centrado y escala aplicada antes de exportar.

---

## Estructura técnica (propuesta)

Entidades principales:
- player
- cameraRig (cámara que sigue al jugador en X)
- enemySpawner (oleadas)
- bulletsPlayer
- bulletsEnemy
- hud (score, vidas, oleada)

Sistemas (JavaScript):
- Input (A/D + disparo)
- Movimiento del jugador
- Spawner de oleadas
- IA de enemigos (formación + ataque)
- Colisiones
- Score y vidas
- Estados del juego (menu, pause, playing, game over)

---

## MVP (mínimo viable por fases)

### MVP 1 (jugable)
- Movimiento A/D
- Disparo
- Enemigos + colisiones + score
- 3 vidas + game over

### MVP 2 (se siente arcade)
- Enemigos atacan (picadas)
- Balas enemigas
- HUD completo

### MVP 3 (presentable)
- 3 tipos de enemigos
- Oleadas con dificultad
- Power-ups y efectos

---

## Objetivo

Recrear el gameplay arcade de GALAGA, manteniendo:
- Controles simples
- Acciones rápidas y claras
- Progresión por oleadas
- Estética atractiva en 3D