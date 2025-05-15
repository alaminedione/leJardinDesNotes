---
title: Guide Complet Hono.js
draft: false
tags:
  - framework
  - web
  - typescript
  - edge-computing
  - serverless
description: Guide complet et référence pratique pour le développement moderne avec Hono.js, incluant des exemples concrets et cas d'utilisation avancés.
---

# Hono.js - Guide Complet du Framework Web Ultra-Rapide

## Vue d'Ensemble

Hono est un framework web léger et performant, spécifiquement conçu pour les environnements d'exécution JavaScript modernes et distribués comme les Edge Workers. Son nom, "flamme" en japonais, évoque sa rapidité et son efficacité. Il se distingue par sa compatibilité avec de multiples plateformes (Cloudflare Workers, Deno, Bun, Node.js), son support TypeScript de premier ordre sans configuration complexe, et son adhésion aux standards Web (Fetch API, Streams, etc.). Hono vise à fournir une expérience de développement simple et productive tout en offrant des performances de pointe pour construire des APIs, des microservices et des applications web.

Ses principaux atouts :

- **Ultra-rapide** : Performances exceptionnelles grâce à son architecture optimisée
- **Multi-runtime** : Fonctionne partout (Cloudflare Workers, Deno, Bun, Node.js)
- **TypeScript natif** : Support TypeScript intégré pour une expérience de développement optimale
- **Standards Web** : Basé sur les Web Standards (Web APIs)
- **Zéro dépendance** : Pas de dépendances externes

## Installation et Configuration

Mettre en place un projet Hono est rapide et s'adapte à votre environnement d'exécution JavaScript préféré. Hono est distribué sous forme de paquet npm standard, mais peut aussi être utilisé directement via l'importation d'URL dans des runtimes comme Deno.

### Installation Standard

L'installation de Hono se fait généralement via un gestionnaire de paquets pour Node.js ou Bun. Pour Deno, qui prend en charge les imports de modules ES via URL, vous pouvez l'importer directement.


```bash
# npm
npm install hono

# pnpm
pnpm add hono

# Deno
import { Hono } from 'https://deno.land/x/hono/mod.ts'
```

### Configuration TypeScript Recommandée

Hono est écrit en TypeScript et offre une excellente expérience de développement typée. Une configuration `tsconfig.json` est recommandée pour bénéficier pleinement de l'autocomplétion et de la vérification de type. Notez l'inclusion des types pour l'environnement de destination si vous n'êtes pas sur Node.js (comme `@cloudflare/workers-types` pour Cloudflare Workers).

```json
{
  "compilerOptions": {
    "target": "ES2019",
    "module": "ES2020",
    "moduleResolution": "node",
    "esModuleInterop": true,
    "strict": true,
    "lib": ["ES2019", "DOM"],
    "types": ["@cloudflare/workers-types"]
  }
}
```

## Fondamentaux

Cette section couvre les éléments de base nécessaires pour construire une application web simple avec Hono, y compris la création d'une instance d'application, l'ajout de middlewares et la définition de routes.

### Application de Base

Une application Hono est créée en instanciant la classe `Hono`. Vous pouvez ensuite utiliser des middlewares et définir des gestionnaires de routes pour différents verbes HTTP et chemins.

```typescript
import { Hono } from 'hono'
import { logger } from 'hono/logger'
import { cors } from 'hono/cors'

const app = new Hono()

// Middlewares globaux
app.use('*', logger())
app.use('/api/*', cors())

// Routes de base
app.get('/', (c) => c.text('Hello Hono!'))
app.post('/api/data', async (c) => {
  const body = await c.req.json()
  return c.json({ received: body })
})

export default app
```

### Système de Routage Avancé

Hono offre un système de routage flexible et puissant qui prend en charge non seulement les chemins statiques, mais aussi les paramètres dynamiques, les expressions régulières et les routes optionnelles. Il permet également d'organiser les routes en groupes pour une meilleure structuration.

```typescript
// Groupes de routes
const api = app.route('/api')

// Routes avec paramètres typés
api.get('/users/:id', (c) => {
  const id: string = c.req.param('id')
  return c.json({ id })
})

// Routes avec expressions régulières
app.get('/articles/:slug{[a-z0-9-]+}', (c) => {
  const slug = c.req.param('slug')
  return c.json({ slug })
})

// Routes optionnelles
app.get('/posts/:id?', (c) => {
  const id = c.req.param('id')
  return c.json({ id: id || 'latest' })
})
```

## Patterns de Design Avancés

Au-delà des fondamentaux, l'architecture de Hono se prête bien à l'application de divers patterns de design pour structurer des applications plus complexes, améliorer la testabilité et organiser le code.

### Injection de Dépendances

L'injection de dépendances est un pattern qui permet de fournir les dépendances (comme des services de base de données, de cache, des loggers, etc.) à un module ou une fonction plutôt que de les laisser les créer elles-mêmes. Dans Hono, cela peut être réalisé en créant l'application avec une fonction factory qui prend les dépendances en argument et les rend disponibles aux gestionnaires de routes via `c.set()`.

```typescript
interface Dependencies {
  db: Database
  cache: Cache
  logger: Logger
}

const createApp = (deps: Dependencies) => {
  const app = new Hono()
  
  app.use('*', async (c, next) => {
    c.set('deps', deps)
    await next()
  })
  
  return app
}

// Usage
const app = createApp({
  db: new Database(),
  cache: new Cache(),
  logger: new Logger()
})
```

### Factory Pattern pour les Routes

Le Factory Pattern peut être appliqué aux routes pour créer des routeurs Hono de manière structurée. Cela est particulièrement utile pour regrouper les routes liées à une ressource ou une fonctionnalité spécifique et leur injecter des dépendances nécessaires, rendant chaque routeur indépendant et testable séparément.

```typescript
interface RouteFactory {
  create: () => Hono
}

class UserRoutes implements RouteFactory {
  constructor(private db: Database) {}
  
  create() {
    const router = new Hono()
    
    router.get('/', (c) => { /* ... */ })
    router.post('/', (c) => { /* ... */ })
    
    return router
  }
}

// Usage
const userRoutes = new UserRoutes(db).create()
app.route('/users', userRoutes)
```

### Architecture Hexagonale

L'Architecture Hexagonale (ou Ports and Adapters) est un pattern qui isole la logique métier principale (le 'noyau') des détails techniques externes (base de données, API externes, UI). Dans le contexte d'une application backend avec Hono, cela implique de définir des 'Ports' (interfaces) pour les interactions externes, et des 'Adapters' (implémentations concrètes) qui réalisent ces interactions. Hono sert ici d'adapter pour l'interface utilisateur (l'API web).

```typescript
// Ports
interface UserRepository {
  findById(id: string): Promise<User>
  save(user: User): Promise<void>
}

// Adapters
class PostgresUserRepository implements UserRepository {
  async findById(id: string): Promise<User> {
    // Implementation
  }
  
  async save(user: User): Promise<void> {
    // Implementation
  }
}

// Application Service
class UserService {
  constructor(private repository: UserRepository) {}
  
  async getUser(id: string): Promise<User> {
    return this.repository.findById(id)
  }
}

// API Routes
const userService = new UserService(new PostgresUserRepository())
app.get('/users/:id', async (c) => {
  const user = await userService.getUser(c.req.param('id'))
  return c.json(user)
})
```

## Intégrations Avancées

Hono, étant agnostique quant à l'environnement d'exécution, s'intègre facilement avec diverses bases de données, caches et services externes. Cette section explore quelques intégrations courantes et avancées.

### Redis Integration

Redis est un store de données in-memory souvent utilisé comme cache, broker de messages ou base de données. Intégrer Redis dans une application Hono est simple, généralement en créant un client Redis et en le rendant accessible aux gestionnaires de routes via le contexte Hono (`c.set()`), similaire à l'injection de dépendances.

```typescript
import { Redis } from '@upstash/redis'

```typescript
import { Redis } from '@upstash/redis'

const redis = new Redis({
  url: 'UPSTASH_REDIS_URL',
  token: 'UPSTASH_REDIS_TOKEN',
})

app.use('*', async (c, next) => {
  c.set('redis', redis)
  await next()
})

app.get('/cache/:key', async (c) => {
  const value = await c.get('redis').get(c.req.param('key'))
  return c.json({ value })
})
```

### WebSocket avec Hono

Les WebSockets permettent une communication bidirectionnelle en temps réel entre le client et le serveur. Hono, en s'appuyant sur les Web Standards et les capacités des runtimes Edge comme Deno et Cloudflare Workers, permet de gérer les connexions WebSocket. L'approche peut varier légèrement selon le runtime utilisé (l'exemple ci-dessous montre l'API spécifique à Deno).

```typescript
app.get('/ws', (c) => {
  if (!c.req.raw.headers.get('Upgrade')) {
    return c.text('Expected Upgrade header')
  }

  const { response, socket } = Deno.upgradeWebSocket(c.req.raw)

```typescript
app.get('/ws', (c) => {
  if (!c.req.raw.headers.get('Upgrade')) {
    return c.text('Expected Upgrade header')
  }

  const { response, socket } = Deno.upgradeWebSocket(c.req.raw)
  
  socket.onmessage = (e) => {
    console.log('received:', e.data)
    socket.send(new Date().toString())
  }
  
  return response
})
```

### RPC avec tRPC

tRPC est un framework qui permet de construire des API end-to-end type-safe sans génération de code. Il s'intègre très bien avec TypeScript et React/Next.js côté client. Hono dispose d'une intégration `@hono/trpc-server` qui permet de lier un routeur tRPC à une route Hono, offrant ainsi une API typée sur votre backend Hono.

```typescript
import { initTRPC } from '@trpc/server'
import { createTRPCHono } from '@hono/trpc-server'

```typescript
import { initTRPC } from '@trpc/server'
import { createTRPCHono } from '@hono/trpc-server'

const t = initTRPC.create()
const router = t.router({
  greeting: t.procedure
    .input((v: unknown) => {
      if (typeof v === 'string') return v
      throw new Error('Invalid input')
    })
    .query((req) => {
      return `Hello, ${req.input}!`
    })
})

const trpcRouter = createTRPCHono({
  router,
  createContext: () => ({})
})

app.use('/trpc/*', trpcRouter)
```

## Tests et Qualité

Assurer la qualité de votre application Hono est essentiel, et les tests automatisés sont un élément clé de ce processus. Hono s\'intègre bien avec les outils de test JavaScript standard.

### Tests Unitaires avec Vitest

Vitest est un framework de test rapide et moderne, compatible avec les projets configurés avec Vite (souvent utilisé avec Hono). Il offre une excellente expérience développeur et s\'intègre facilement. Pour tester vos gestionnaires de routes ou vos middlewares en isolation, Hono fournit une méthode `app.request()` qui simule une requête HTTP, sans avoir besoin d\'un vrai serveur.

```typescript
import { describe, it, expect } from 'vitest'
import { app } from './app'

describe('API Tests', () => {
  it('should return hello world', async () => {
    const res = await app.request('/')
    expect(res.status).toBe(200)
    expect(await res.text()).toBe('Hello Hono!')
  })
  
  it('should handle JSON', async () => {
    const res = await app.request('/api/data', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ test: true })
    })
    
    expect(res.status).toBe(200)
    expect(await res.json()).toEqual({
      received: { test: true }
    })
  })
})
```

### Tests d\'Intégration

Les tests d\'intégration visent à vérifier que différentes parties de votre application (par exemple, Hono interagissant avec une base de données ou un autre service) fonctionnent correctement ensemble. Vous pouvez utiliser le même environnement de test (comme Vitest) et la méthode `app.request()`, mais en configurant un environnement qui inclut les dépendances externes nécessaires (bases de données de test, services mockés, etc.).

```typescript
import { beforeAll, afterAll } from 'vitest'
import { app } from './app'
import { startTestDb, stopTestDb } from './test-utils'

beforeAll(async () => {
  await startTestDb()
})

afterAll(async () => {
  await stopTestDb()
})

describe('Integration Tests', () => {
  it('should create and retrieve user', async () => {
    // Create user
    const createRes = await app.request('/api/users', {
      method: 'POST',
      body: JSON.stringify({
        name: 'Test User',
        email: 'test@example.com'
      })
    })
    
    expect(createRes.status).toBe(201)
    const { id } = await createRes.json()
    
    // Retrieve user
    const getRes = await app.request(`/api/users/${id}`)
    expect(getRes.status).toBe(200)
    
    const user = await getRes.json()
    expect(user).toEqual({
      id,
      name: 'Test User',
      email: 'test@example.com'
    })
  })
})
```

## Monitoring et Observabilité

Dans un environnement de production, il est crucial de surveiller les performances et le comportement de votre application Hono. L'observabilité, comprenant les métriques, le tracing et le logging, permet de comprendre ce qui se passe à l'intérieur de l'application.

### OpenTelemetry Integration

```typescript
import { trace } from '@opentelemetry/api'
// Assuming you have an OpenTelemetry middleware
// import { OpenTelemetryMiddleware } from './middleware/opentelemetry'

const tracer = trace.getTracer('hono-app')

// app.use('*', OpenTelemetryMiddleware())

app.get('/traced-route', async (c) => {
  // Example usage of OpenTelemetry API
  const span = tracer.startSpan('business-logic')
  
  try {
    // Business logic here
    return c.json({ status: 'success' })
  } finally {
    span.end()
  }
})

### Monitoring Middleware

Ce middleware illustre comment collecter des métriques de base (nombre de requêtes, nombre d'erreurs, durée des requêtes) dans une application Hono. Notez que pour une solution de monitoring en production, il est préférable d'utiliser une bibliothèque dédiée qui exportera ces métriques vers un système de collecte et de visualisation (par exemple, Prometheus, Grafana).

```typescript
const metrics = {
  requestCount: 0,
  errorCount: 0,
  requestDuration: new Map<string, number[]>()
}

// This middleware tracks request counts, errors, and durations
app.use('*', async (c, next) => {
  const start = performance.now()
  try {
    await next()
    metrics.requestCount++
  } catch (err) {
    metrics.errorCount++
    throw err
  } finally {
    const duration = performance.now() - start
    const path = c.req.path

    if (!metrics.requestDuration.has(path)) {
      metrics.requestDuration.set(path, [])
    }
    metrics.requestDuration.get(path)?.push(duration)
  }
})

// Endpoint to expose collected metrics
app.get('/metrics', (c) => {
  return c.json(metrics)
})
```

## Optimisations Avancées

### Streaming JSON

Le streaming JSON permet d'envoyer des données JSON au client en plusieurs morceaux (chunks) plutôt que d'attendre que toutes les données soient prêtes avant d'envoyer une seule réponse. Cela peut améliorer la performance perçue, en particulier pour les grandes quantités de données. Hono prend en charge le streaming via l'API `ReadableStream`.

```typescript
app.get('/stream-data', (c) => {
  const stream = new ReadableStream({
    async start(controller) {
      for (let i = 0; i < 100; i++) {
        controller.enqueue(JSON.stringify({ count: i }) + '\n')
        await new Promise(r => setTimeout(r, 100))

```typescript
app.get('/stream-data', (c) => {
  const stream = new ReadableStream({
    async start(controller) {
      for (let i = 0; i < 100; i++) {
        controller.enqueue(JSON.stringify({ count: i }) + '\n')
        await new Promise(r => setTimeout(r, 100))
      }
      controller.close()
    }
  })

  return new Response(stream, {
    headers: {
      'Content-Type': 'application/x-ndjson',
      'Transfer-Encoding': 'chunked'
    }
  })
})
```

### Cache Control

La gestion du cache est essentielle pour améliorer la performance des applications web. En définissant des en-têtes `Cache-Control`, vous pouvez indiquer aux navigateurs et aux CDNs comment mettre en cache les réponses, réduisant ainsi la charge sur le serveur et améliorant l'expérience utilisateur.

```typescript
const cacheControl = (maxAge: number) => async (c: Context, next: Next) => {
  await next()

```typescript
const cacheControl = (maxAge: number) => async (c: Context, next: Next) => {
  await next()
  
  if (c.res.headers.get('Cache-Control')) {
    // Skip if Cache-Control is already set
    return;
  }

  if (c.res.headers.get('Content-Type')?.includes('application/json')) {
    c.res.headers.set('Cache-Control', `public, max-age=${maxAge}`)
  }
}

app.use('/api/*', cacheControl(3600)) // 1 hour cache
```

### Response Compression

La compression des réponses HTTP (gzip, Brotli) réduit la taille des données transférées entre le serveur et le client, ce qui améliore le temps de chargement des pages. Hono fournit un middleware `compress` pour activer la compression des réponses.

```typescript
import { compress } from 'hono/compress'

```typescript
import { compress } from 'hono/compress'

app.use('*', compress({
  encoding: 'gzip',
  minLength: 1024, // Only compress responses larger than 1KB
  // Exclude certain content types
  excludeContentType: [
    'image/',
    'video/',
    'audio/'
  ]
}))
```

## Déploiement Multi-Cloud

Hono facilite le déploiement de vos applications sur diverses plateformes cloud, y compris les environnements serverless. Voici quelques exemples de déploiement sur les plateformes les plus populaires.

### AWS Lambda

AWS Lambda est un service de calcul serverless qui vous permet d'exécuter du code sans provisionner ni gérer de serveurs. Pour déployer une application Hono sur AWS Lambda, vous devez utiliser le wrapper `hono/aws-lambda` pour adapter l'application Hono à la fonction Lambda.

```typescript
import { Hono } from 'hono'
import { handle } from 'hono/aws-lambda'

const app = new Hono()

// Routes...

// Export the handler function for AWS Lambda
export const handler = handle(app)
```

<old_text>
### Google Cloud Functions

```typescript
import { Hono } from 'hono'
import { handle } from '@hono/node-server/gcf'

const app = new Hono()

### Google Cloud Functions

```typescript
import { Hono } from 'hono'
import { handle } from '@hono/node-server/gcf'

const app = new Hono()

// Routes...

// Export the handler function for Google Cloud Functions
export const handler = handle(app)
```

<old_text>
### Azure Functions

```typescript
import { Hono } from 'hono'
import { handle } from '@hono/node-server/azure'

const app = new Hono()

### Azure Functions

```typescript
import { Hono } from 'hono'
import { handle } from '@hono/node-server/azure'

const app = new Hono()

// Routes...

// Export the handler function for Azure Functions
export default handle(app)
```

</edits>
```

## Sécurité Avancée

La sécurité est un aspect crucial du développement web. Hono, bien qu'étant un framework minimaliste, permet d'intégrer facilement diverses mesures de sécurité pour protéger vos applications.

### Rate Limiting avec Redis

La limitation du débit (rate limiting) permet de protéger votre API contre les abus et les attaques par déni de service (DoS) en limitant le nombre de requêtes qu'un client peut effectuer dans un laps de temps donné. Cet exemple utilise Redis pour stocker et incrémenter le nombre de requêtes par adresse IP.

```typescript
import { Redis } from '@upstash/redis'

const rateLimit = (redis: Redis, limit: number, window: number) => {
  return async (c: Context, next: Next) => {
    const ip = c.req.header('x-forwarded-for') || 'unknown'
    const key = `rate-limit:${ip}`
    
    const current = await redis.incr(key)
    if (current === 1) {
      await redis.expire(key, window)
    }
    
    if (current > limit) {
      return c.json({ 
        error: 'Too many requests',
        retryAfter: await redis.ttl(key)
      }, 429)
    }
    
    await next()
  }
}

app.use('*', rateLimit(redis, 100, 3600)) // 100 requests per hour
```

### CSRF Protection

La protection contre les attaques Cross-Site Request Forgery (CSRF) est essentielle pour les applications web qui gèrent des états (par exemple, les sessions utilisateur). Les attaques CSRF exploitent la confiance qu'un site web a envers le navigateur d'un utilisateur. Le middleware `hono/csrf` permet de générer et de valider des tokens CSRF pour chaque requête, empêchant ainsi les attaques CSRF.

```typescript
import { csrf } from 'hono/csrf'

app.use('/api/*', csrf({
  origin: 'https://example.com',
  methods: ['POST', 'PUT', 'DELETE'],
  tokenKey: 'csrf-token'
}))
```

### Content Security Policy

La Content Security Policy (CSP) est un en-tête HTTP qui permet de contrôler les ressources (scripts, styles, images, etc.) qu'un navigateur est autorisé à charger pour une page web donnée. Cela permet de réduire considérablement le risque d'attaques XSS (Cross-Site Scripting).

```typescript
app.use('*', async (c, next) => {
  await next()
  
  c.header('Content-Security-Policy', [
    "default-src 'self'",
    "script-src 'self' 'unsafe-inline' 'unsafe-eval'",
    "style-src 'self' 'unsafe-inline'",
    "img-src 'self' data: https:",
    "connect-src 'self' https://api.example.com"
  ].join('; '))
})
```

## Maintenance et Mises à Jour

La maintenance et les mises à jour sont des aspects importants du cycle de vie d'une application web. Cette section décrit comment gérer les migrations de base de données et les vérifications de l'état de santé (health checks) dans une application Hono.

### Scripts de Migration

Les scripts de migration sont essentiels pour faire évoluer le schéma de votre base de données de manière contrôlée. Ils permettent d'appliquer des changements de schéma, d'ajouter ou de supprimer des tables ou des colonnes, et de mettre à jour les données existantes. Cet exemple montre comment organiser et exécuter des migrations dans une application Hono.

```typescript
interface Migration {
  up: () => Promise<void>
  down: () => Promise<void>
}

const migrations: Record<string, Migration> = {
  '001_initial': {
    up: async () => {
      // Migration logic
    },
    down: async () => {
      // Rollback logic
    }
  }
}

app.post('/admin/migrate/:version', async (c) => {
  const version = c.req.param('version')
  const migration = migrations[version]
  
  if (!migration) {
    return c.json({ error: 'Migration not found' }, 404)
  }
  
  try {
    await migration.up()
    return c.json({ status: 'success' })
  } catch (error) {
    await migration.down()
    throw error
  }
})
```

### Health Checks

Les vérifications de l'état de santé (health checks) permettent de surveiller la disponibilité et le bon fonctionnement de votre application et de ses dépendances. Elles sont utilisées par les systèmes d'orchestration de conteneurs (comme Kubernetes) et les équilibreurs de charge (load balancers) pour déterminer si une instance de l'application est saine et capable de traiter les requêtes.

```typescript
interface HealthCheck {
  name: string
  check: () => Promise<boolean>
}

const healthChecks: HealthCheck[] = [
  {
    name: 'database',
    check: async () => {
      try {
        await db.ping()
        return true
      } catch {
        return false
      }
    }
  },
  {
    name: 'redis',
    check: async () => {
      try {
        await redis.ping()
        return true
      } catch {
        return false
      }
    }
  }
]

app.get('/health', async (c) => {
  const results = await Promise.all(
    healthChecks.map(async ({ name, check }) => ({
      name,
      status: await check() ? 'healthy' : 'unhealthy'
    }))
  )
  
  const allHealthy = results.every(r => r.status === 'healthy')
  
  return c.json({
    status: allHealthy ? 'healthy' : 'unhealthy',
    checks: results
  }, allHealthy ? 200 : 503)
})
```

## Ressources et Liens Utiles

- [Documentation Officielle](https://hono.dev)
- [GitHub Repository](https://github.com/honojs/hono)
- [Examples](https://github.com/honojs/examples)
- [Discord Community](https://discord.gg/KQh8xZyknB)

## Notes de Maintenance

Ce guide est régulièrement mis à jour pour refléter les meilleures pratiques et les nouvelles fonctionnalités de Hono. Pour toute suggestion ou correction, n'hésitez pas à contribuer via GitHub.

Dernière mise à jour : 2024-01