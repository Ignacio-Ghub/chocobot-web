# Choco World — Sommelier de Cacao 🍫

> Landing page de e-commerce artesanal con ChocoBot: agente de ventas inteligente y sommelier digital de chocolate fino, potenciado por IA y automatización con n8n.

---

## ¿Qué hace esta app?

**Choco World** es una tienda conceptual de chocolates de origen venezolano con un asistente de ventas inteligente integrado. Cuando un cliente interactúa con ChocoBot:

1. **Recibe la consulta** — vía chat web embebido en la página o vía Telegram
2. **Analiza el mensaje** — texto o imagen (visión computacional con GPT-4o)
3. **Actúa como sommelier** — recomienda productos según perfil de sabor, hace cross-selling y cualifica al cliente
4. **Gestiona el pedido completo** — recoge nombre, email, teléfono y dirección
5. **Ejecuta automáticamente** dos acciones al confirmar el pedido:
   - Envía email de confirmación al cliente con resumen y link de pago
   - Guarda todos los datos del cliente en Google Sheets

---

## Canales disponibles

| Canal | Descripción |
|---|---|
| Chat web | Widget n8n embebido directamente en la landing page |
| Telegram | Bot conectado al mismo agente IA, con soporte de imágenes |

---

## Stack técnico

| Capa | Tecnología |
|---|---|
| Frontend | HTML5 + CSS3 + JavaScript vanilla |
| Chat widget | @n8n/chat (librería oficial de n8n) |
| Automatización | n8n (hosted) |
| IA | GPT-4o via OpenAI API |
| Memoria conversacional | Window Buffer Memory (n8n) |
| Base de datos pedidos | Google Sheets |
| Email de confirmación | Gmail API |
| Canal adicional | Telegram Bot |

---

## Arquitectura del agente IA

```
Chat Web (n8n widget)
Telegram Bot
        ↓
  [Check if Photo]
        ├── SÍ → Get Telegram File → Prepare Image → AI Agent
        └── NO → Prepare Input → AI Agent
                      ↓
            AI Agent (Manager) — GPT-4o
            ├── Window Buffer Memory (contexto conversacional)
            ├── Gmail Tool (envío de confirmación)
            └── Google Sheets Tool (registro de pedido)
                      ↓
              [If Telegram?]
                ├── SÍ → Send Agent Response (Telegram)
                └── NO → Respuesta automática (chat web)
```

---

## Catálogo de productos

| Producto | Precio | Perfil |
|---|---|---|
| 🍫 Trufas de Cacao 70% | €19,99 | Intenso · Amargo · Sofisticado |
| 🍊 Bombones de Maracuyá | €14,99 | Cítrico · Dulce · Exótico |
| 🧂 Barras de Sal Marina | €9,99 | Crocante · Dulce-Salado · Equilibrado |

---

## Capacidades de ChocoBot

**Sommelier digital**
- Recomienda productos según perfil de sabor del cliente
- Explica terroir, fermentación y proceso de cada tableta
- Sugiere maridajes con vinos, licores y alimentos

**Visión computacional**
- Analiza imágenes enviadas por el cliente
- Correlaciona visualmente con productos del catálogo
- Argumenta la recomendación basada en la imagen

**Ventas consultivas**
- Cross-selling estratégico para elevar ticket promedio
- Preguntas de cualificación para personalizar la recomendación
- Cierre transaccional automatizado

**Gestión de pedidos**
- Recopila datos completos del cliente conversacionalmente
- Dispara automáticamente email de confirmación + registro en Sheets
- Multilingüe

---

## Estructura del proyecto

```
choco-world/
├── index.html     # Landing page completa + chat widget integrado
└── README.md
```

---

## Credenciales necesarias en n8n

| Servicio | Tipo |
|---|---|
| OpenAI | API Key |
| Gmail | OAuth2 |
| Google Sheets | OAuth2 |
| Telegram | Bot Token |

Todas las credenciales están almacenadas en n8n — ninguna aparece en el código fuente.

---

## Seguridad

- Todas las credenciales de servicios están encriptadas en n8n
- El código HTML no contiene tokens, API keys ni contraseñas
- La URL del chat widget es pública por diseño del widget oficial de n8n
- El agente tiene protocolos de bloqueo ante contenido inapropiado (NSFW, violencia)

---

## Roadmap

- [ ] Integración con pasarela de pago real (Stripe)
- [ ] Panel de pedidos en Google Sheets con estados (pendiente, enviado, entregado)
- [ ] Ampliar catálogo con más orígenes (Madagascar, Ecuador, Ghana)
- [ ] Notificación al equipo de operaciones vía Slack al confirmar pedido
- [ ] Sistema de descuentos y códigos promocionales

---

## Autor

**Jesús Ignacio Briceño Alarcón**  
Consultor en Derechos Humanos & Cooperación Internacional  
Director & Co-fundador — Humanita's Foundation e.V. (Alemania)  
Basado en los Países Bajos · Disponible internacionalmente

---

*Construido con HTML vanilla + n8n + GPT-4o · Proyecto de portfolio*
