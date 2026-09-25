# Elite Esco — Agencia de Landing Pages

## Identidad de la Agencia

**Nombre**: Elite Esco  
**Propósito**: Creación de landing pages de alto impacto para empresas cliente.  
**Mercado principal**: Colombia  
**Modelo de negocio**: Cada landing page que se construye para un cliente incluye pasarela de pagos integrada.

---

## Stack Tecnológico Recomendado

### Framework & Frontend
- **Next.js 15** (App Router) — SSR/SSG para SEO óptimo, crítico en landing pages
- **React 19** + **TypeScript** — base sólida y tipado estricto
- **Tailwind CSS** — velocidad de desarrollo + consistencia visual
- **Framer Motion** — animaciones y microinteracciones que convierten
- **shadcn/ui** — componentes accesibles y personalizables

### CMS / Gestión de contenido
- **Sanity.io** — CMS headless flexible, el cliente edita su propia landing sin tocar código
- **Contentful** (alternativa) — si el cliente prefiere interfaz más tradicional

### Formularios y Conversión
- **React Hook Form** + **Zod** — validación de formularios robusta
- **HubSpot Forms** (opcional) — si el cliente ya usa HubSpot como CRM
- **Resend** — envío de emails transaccionales (confirmaciones, leads)

### Analytics & Tracking
- **Google Analytics 4** — métricas estándar
- **Meta Pixel** — tracking para campañas de Facebook/Instagram
- **Hotjar** o **Microsoft Clarity** — mapas de calor y grabación de sesiones
- **Vercel Analytics** — Web Vitals en tiempo real

### Hosting & Infraestructura
- **Vercel** — deploy automático, CDN global, dominio personalizado
- **Cloudflare** — DNS + protección DDoS + caché adicional

---

## Pasarelas de Pago — Colombia

Cada landing page de Elite Esco debe incluir una pasarela de pagos. Opciones por perfil de cliente:

### 1. Wompi (Recomendada — Bancolombia)
- **Ideal para**: PyMEs y startups colombianas
- **Métodos**: Tarjeta crédito/débito, PSE, Nequi, Bancolombia QR, efectivo (Efecty)
- **Integración**: SDK JS o API REST
- **Comisión**: ~2.9% + $900 COP por transacción
- **Docs**: https://docs.wompi.co
- **Ventaja**: Respaldo de Bancolombia, alta confianza del usuario colombiano

### 2. PayU Colombia
- **Ideal para**: Empresas medianas y grandes con volumen alto
- **Métodos**: Tarjetas, PSE, Nequi, Daviplata, Efecty, Baloto
- **Integración**: SDK, API REST, formulario hosted
- **Comisión**: Variable según contrato (~3.49%)
- **Ventaja**: Líder histórico en LatAm, soporte robusto

### 3. Epayco
- **Ideal para**: Emprendedores y pequeños negocios
- **Métodos**: Tarjetas, PSE, Efecty, Baloto, Nequi
- **Comisión**: 2.99% + IVA
- **Ventaja**: Fácil integración, bajo costo de entrada

### 4. Mercado Pago Colombia
- **Ideal para**: Clientes que ya venden en Mercado Libre o con alta adopción de billetera digital
- **Métodos**: Tarjetas, PSE, efectivo, QR
- **Ventaja**: Red amplia, checkout reutilizable

### 5. Stripe (con localización Colombia)
- **Ideal para**: Clientes con ventas internacionales además de Colombia
- **Nota**: Requiere empresa con cuenta bancaria que acepte USD; complementar con Wompi para pagos locales

---

## Estructura de Proyecto — Landing Page Tipo

```
elite-esco-[cliente]/
├── app/
│   ├── (landing)/
│   │   ├── page.tsx          # Landing principal
│   │   └── gracias/page.tsx  # Página de confirmación post-pago
│   ├── api/
│   │   ├── pagos/route.ts    # Webhook pasarela de pagos
│   │   └── leads/route.ts    # Captura de leads
│   └── layout.tsx
├── components/
│   ├── Hero.tsx
│   ├── Beneficios.tsx
│   ├── Testimonios.tsx
│   ├── Precios.tsx
│   ├── CTA.tsx
│   └── checkout/
│       └── BotonPago.tsx     # Integración pasarela
├── lib/
│   ├── wompi.ts              # Utilidades pasarela
│   └── analytics.ts
├── public/
└── CLAUDE.md
```

---

## Secciones Estándar de una Landing Page Elite Esco

1. **Hero** — Propuesta de valor clara + CTA principal
2. **Problema/Dolor** — Conectar con el usuario
3. **Solución / Beneficios** — Qué ofrece el cliente
4. **Cómo funciona** — Pasos simples (3–5 pasos)
5. **Prueba social** — Testimonios, logos, métricas
6. **Precios** — Tabla de planes o precio único
7. **FAQ** — Objeciones frecuentes
8. **CTA final** — Llamado a la acción con urgencia
9. **Footer** — Políticas, contacto, redes

---

## Variables de Entorno Requeridas por Proyecto

```env
# Pasarela de pagos (Wompi ejemplo)
WOMPI_PUBLIC_KEY=
WOMPI_PRIVATE_KEY=
WOMPI_EVENTS_SECRET=

# Email
RESEND_API_KEY=

# Analytics
NEXT_PUBLIC_GA_ID=
NEXT_PUBLIC_META_PIXEL_ID=

# CMS (si aplica)
SANITY_PROJECT_ID=
SANITY_DATASET=
SANITY_TOKEN=
```

---

## Convenciones de Desarrollo

- **Naming**: camelCase en JS/TS, kebab-case en rutas y archivos de componentes
- **Commits**: Convencional Commits (`feat:`, `fix:`, `chore:`)
- **Branch por cliente**: `feat/cliente-[nombre]`
- **Testing**: Vitest + Playwright para flujo de pago crítico
- **SEO**: `generateMetadata` en cada page.tsx, Open Graph, sitemap.xml
- **Performance**: Core Web Vitals > 90 en Lighthouse antes de entregar

---

## Proceso de Entrega a Cliente

1. Briefing + definición de pasarela de pagos
2. Diseño en Figma (aprobación cliente)
3. Desarrollo (Next.js + pasarela)
4. Pruebas de pago en sandbox
5. Deploy en Vercel + dominio del cliente
6. Capacitación en CMS (si aplica)
7. Entrega de accesos y documentación

---

## Notas Importantes

- Siempre validar el webhook de la pasarela con firma criptográfica antes de procesar
- Las políticas de tratamiento de datos (Ley 1581 de 2012 — Colombia) son obligatorias en toda landing
- Incluir política de privacidad y términos y condiciones como páginas separadas
- Toda landing debe tener SSL (Vercel lo provee automáticamente)
