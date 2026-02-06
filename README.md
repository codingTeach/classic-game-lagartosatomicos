# GALAGA 3D (Tercera Persona) — Diseño y Mecánicas

Este proyecto busca recrear la esencia del clásico **GALAGA**, pero en un entorno **3D** accesible desde el navegador usando **A-Frame + HTML/CSS/JavaScript**.  
El enfoque de gameplay mantiene la jugabilidad arcade: **controles simples, oleadas de enemigos, disparo constante y puntaje**.

---

## 🎮 Concepto de Juego

**Shooter espacial 3D en tercera persona (desde la espalda)** donde el jugador controla una nave que:
- Se mueve **solo lateralmente (izquierda/derecha)**.
- Dispara hacia el frente para destruir enemigos.
- Sobrevive a oleadas con dificultad creciente.
- Acumula puntos y (opcionalmente) mejora su nave con power-ups.

---

## 🕹️ Controles

- **A** → Mover izquierda
- **D** → Mover derecha
- **Space** → Disparar
- **P / ESC** → Pausa (opcional)

> *El movimiento es únicamente en el eje X (lateral).*

---

## 📷 Cámara (Tercera Persona)

La cámara se ubica **detrás del jugador** (vista desde la espalda), con estas reglas:

- Sigue al jugador **solo en X** (suavemente).
- Mantiene una distancia fija en Z y una altura fija en Y.
- Siempre mira hacia el frente (zona donde aparecen los enemigos).

✅ Esto permite ver modelos 3D y profundidad, sin complicar el control.

---

## 🚀 Movimiento del Jugador (Solo Lateral)

- Movimiento: **eje X** únicamente.
- Límites del escenario:
  - Ejemplo: `X ∈ [-8, 8]` (ajustable según el tamaño de tu escena).
- Feeling recomendado:
  - **Aceleración suave** al moverse
  - **Frenado suave** al soltar teclas
  - Velocidad máxima fija para mantener estilo arcade

---

## 🔫 Disparo y Combate

### Disparo del jugador
- Disparo recto hacia el frente (eje Z).
- Cadencia (cooldown): **200–300 ms**.
- Las balas desaparecen si:
  - salen del rango (distancia máxima)
  - chocan con un enemigo

### Enemigos
Los enemigos manejan dos estados principales:

1. **Formación**
   - Se mueven en grupo con patrón tipo “wave” (oscilación).
2. **Ataque**
   - 1–2 enemigos se desprenden y hacen “picadas” hacia el jugador (curva simple).

### Disparo enemigo (opcional pero recomendado)
- Balas lentas y visibles.
- Frecuencia baja al inicio (sube por nivel).

---

## 💥 Colisiones (Reglas)

El jugador pierde vida si:
- Choca con un enemigo.
- Recibe un proyectil enemigo.

El enemigo muere si:
- Recibe un proyectil del jugador.

✅ Recomendación técnica: usar **hitboxes simples** (esfera/caja invisible) en vez de colisión por malla.

---

## ❤️ Vidas y Game Over

- Vidas iniciales: **3**
- Al perder vida:
  - Explosión / efecto visual
  - **Invulnerabilidad temporal (≈1 segundo)** con parpadeo
- **Game Over** cuando las vidas llegan a 0.

---

## ⭐ Puntaje (Score)

Puntajes sugeridos:

- Enemigo básico: **50**
- Enemigo rápido: **100**
- Enemigo tanque: **200**

Opcional:
- Vida extra cada X puntos (ej. 10,000)
- Bonos por combos

---

## 📈 Progresión por Oleadas (Dificultad)

Cada oleada puede aumentar la dificultad con:

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

## 👾 Tipos de Enemigos (Mínimos)

1. **Básico (1 hit)**
   - formación + ataques ocasionales
2. **Rápido (1 hit)**
   - zig-zag corto o movimientos más rápidos
3. **Tanque (3 hits)**
   - lento, más resistente, puede disparar más

---

## 🎁 Power-Ups (Opcional)

Power-ups simples para mantener el estilo arcade:

- **Double Shot** (disparo doble por 10s)
- **Rapid Fire** (cadencia más rápida por 8–10s)
- **Shield** (absorbe 1 golpe)

Drop chance: **10–20%** al destruir enemigos especiales.

---

## 🌌 Escenario 3D (Sensación de Profundidad)

Para que se sienta 3D aunque el movimiento sea lateral:

- Skybox/sky con estrellas
- Plano/pista sutil (grid tenue o piso oscuro)
- Efecto de velocidad:
  - partículas de estrellas moviéndose hacia el jugador
  - líneas de luz / túnel espacial

---

## 🧊 Modelos 3D (Blender)

Modelos recomendados (low poly):

- Nave del jugador (player ship)
- 3 tipos de naves enemigas (básico, rápido, tanque)
- Bala del jugador / bala enemiga
- Power-up (capsula/cubo)
- Explosión (sprite o partículas)

✅ Formato recomendado: **.glb / glTF**  
✅ Importante: pivot/origen centrado y escala aplicada antes de exportar.

---

## 🧠 Estructura Técnica (Propuesta)

Entidades principales:
- `player`
- `cameraRig` (cámara que sigue al jugador en X)
- `enemySpawner` (oleadas)
- `bulletsPlayer`
- `bulletsEnemy`
- `hud` (score / vidas / oleada)

Sistemas (JS):
- Input (A/D + disparo)
- Movimiento del player
- Spawner de oleadas
- IA de enemigos (formación + ataque)
- Colisiones
- Score / vidas
- Estados del juego (menu, pause, playing, game over)

---

## ✅ MVP (Mínimo Viable por Fases)

### MVP 1 — Jugable
- Movimiento A/D
- Disparo
- Enemigos + colisiones + score
- 3 vidas + game over

### MVP 2 — Se siente arcade
- Enemigos atacan (picadas)
- Balas enemigas
- HUD completo

### MVP 3 — Proyecto presentable
- 3 tipos de enemigos
- Oleadas con dificultad
- Power-ups y efectos

---

## 📌 Objetivo

Recrear el gameplay arcade de GALAGA, manteniendo:
- Controles simples
- Acciones rápidas y claras
- Progresión por oleadas
- Estética atractiva en 3D
