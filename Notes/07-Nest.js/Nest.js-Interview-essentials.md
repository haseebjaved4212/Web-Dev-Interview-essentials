#  NestJS Interview Essentials

> A complete, beginner-friendly reference guide covering every NestJS concept you need to ace backend and full-stack developer interviews. Written in simple, easy English with clear code examples and real-world patterns.

---

## 📌 Table of Contents

- [What is NestJS?](#what-is-nestjs)
- [Why Use NestJS?](#why-use-nestjs)
- [Project Structure](#project-structure)
- [Modules](#modules)
- [Controllers](#controllers)
- [Providers and Services](#providers-and-services)
- [Dependency Injection](#dependency-injection)
- [Request Lifecycle](#request-lifecycle)
- [DTOs and Validation](#dtos-and-validation)
- [Pipes](#pipes)
- [Guards](#guards)
- [Interceptors](#interceptors)
- [Exception Filters](#exception-filters)
- [Middleware](#middleware)
- [Custom Decorators](#custom-decorators)
- [Database Integration (TypeORM)](#database-integration-typeorm)
- [Database Integration (Prisma)](#database-integration-prisma)
- [Authentication with JWT](#authentication-with-jwt)
- [Authorization and Roles](#authorization-and-roles)
- [Configuration Management](#configuration-management)
- [Microservices](#microservices)
- [WebSockets (Gateways)](#websockets-gateways)
- [GraphQL in NestJS](#graphql-in-nestjs)
- [File Uploads](#file-uploads)
- [Caching](#caching)
- [Task Scheduling (Cron Jobs)](#task-scheduling-cron-jobs)
- [Testing in NestJS](#testing-in-nestjs)
- [Swagger / API Documentation](#swagger--api-documentation)
- [Logging](#logging)
- [Best Practices](#best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is NestJS?

NestJS is a **backend framework for building Node.js server-side applications**, written in and fully supporting TypeScript. Think of it as the "Angular for the backend" — it brings the same kind of organized, modular, opinionated structure that Angular brought to frontend development, but for building APIs and server applications.

Under the hood, NestJS uses **Express** by default (you can switch to Fastify for better performance), but it adds a powerful architecture on top with modules, dependency injection, decorators, and a clean separation of concerns.

```typescript
// A simple NestJS controller — this is what NestJS code looks like
import { Controller, Get, Param } from "@nestjs/common";

@Controller("users")
export class UsersController {
  @Get(":id")
  getUser(@Param("id") id: string) {
    return { id, name: "Haseeb" };
  }
}
```

If you compare this to raw Express, you can see NestJS gives you structure, decorators, and built-in patterns instead of you having to set everything up by hand.

---

## Why Use NestJS?

- **TypeScript-first** — full type safety throughout your backend
- **Organized architecture** — modules, controllers, services keep code clean and scalable
- **Dependency Injection built-in** — makes testing and swapping implementations easy
- **Works with Express or Fastify** — pick the HTTP engine you prefer
- **Built-in support** for GraphQL, WebSockets, microservices, and gRPC
- **Great for large teams** — opinionated structure means everyone writes code the same way
- **Huge ecosystem** — official packages for auth, config, caching, queues, scheduling

### NestJS vs Express vs Plain Node.js

| | Plain Node.js | Express | NestJS |
|---|---|---|---|
| Structure | None, you build it | Minimal, flexible | Opinionated, organized |
| TypeScript | Manual setup | Manual setup | Built-in |
| Dependency Injection | No | No | Yes, built-in |
| Best for | Learning fundamentals | Small to medium apps | Medium to large, enterprise apps |
| Learning curve | Low | Low | Medium to high |

> **Interview Tip:** A common interview answer is: "Express gives you freedom but no structure, which can become messy in large teams. NestJS gives you an opinionated, testable architecture out of the box, similar to how Angular structures frontend apps, which makes it ideal for large or long-term projects."

---

## Project Structure

```
src/
├── main.ts                    ← Entry point, bootstraps the app
├── app.module.ts              ← Root module
├── app.controller.ts          ← Root controller (often removed in real apps)
├── app.service.ts             ← Root service
├── users/
│   ├── users.module.ts        ← Feature module
│   ├── users.controller.ts    ← Handles HTTP requests
│   ├── users.service.ts       ← Business logic
│   ├── users.repository.ts    ← Database queries (optional pattern)
│   ├── dto/
│   │   ├── create-user.dto.ts
│   │   └── update-user.dto.ts
│   ├── entities/
│   │   └── user.entity.ts     ← Database model (TypeORM)
│   └── users.controller.spec.ts  ← Unit tests
├── auth/
│   ├── auth.module.ts
│   ├── auth.service.ts
│   ├── auth.controller.ts
│   ├── guards/
│   │   └── jwt-auth.guard.ts
│   └── strategies/
│       └── jwt.strategy.ts
├── common/
│   ├── decorators/
│   ├── filters/
│   ├── guards/
│   ├── interceptors/
│   └── pipes/
└── config/
    └── configuration.ts
```

### main.ts — Entry point

```typescript
// main.ts
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";
import { ValidationPipe } from "@nestjs/common";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // Global validation pipe (validates all incoming DTOs automatically)
  app.useGlobalPipes(new ValidationPipe({
    whitelist: true,            // strips properties not in the DTO
    forbidNonWhitelisted: true, // throws error for extra properties
    transform: true,            // auto-transform payloads to DTO instances
  }));

  // Enable CORS
  app.enableCors();

  // Set a global prefix for all routes
  app.setGlobalPrefix("api/v1");

  await app.listen(3000);
  console.log("Application running on http://localhost:3000");
}

bootstrap();
```

---

## Modules

Modules are how NestJS **organizes your application into related chunks**. Every Nest app has at least one module, the root module. Each feature (users, products, orders) usually gets its own module.

```typescript
// users.module.ts
import { Module } from "@nestjs/common";
import { UsersController } from "./users.controller";
import { UsersService } from "./users.service";
import { TypeOrmModule } from "@nestjs/typeorm";
import { User } from "./entities/user.entity";

@Module({
  imports: [TypeOrmModule.forFeature([User])],  // other modules this one depends on
  controllers: [UsersController],                // controllers belonging to this module
  providers: [UsersService],                      // services/providers in this module
  exports: [UsersService],                        // make UsersService available to OTHER modules
})
export class UsersModule {}
```

```typescript
// app.module.ts — the root module that ties everything together
import { Module } from "@nestjs/common";
import { UsersModule } from "./users/users.module";
import { AuthModule } from "./auth/auth.module";
import { ProductsModule } from "./products/products.module";
import { ConfigModule } from "@nestjs/config";
import { TypeOrmModule } from "@nestjs/typeorm";

@Module({
  imports: [
    ConfigModule.forRoot({ isGlobal: true }),
    TypeOrmModule.forRoot({
      type: "postgres",
      host: "localhost",
      port: 5432,
      username: "postgres",
      password: "password",
      database: "myapp",
      autoLoadEntities: true,
      synchronize: true,  // never use true in production!
    }),
    UsersModule,
    AuthModule,
    ProductsModule,
  ],
})
export class AppModule {}
```

### Global Modules

```typescript
// A module marked @Global() is available everywhere WITHOUT needing to import it
import { Global, Module } from "@nestjs/common";

@Global()
@Module({
  providers: [DatabaseService],
  exports: [DatabaseService],
})
export class DatabaseModule {}
// Now DatabaseService can be injected anywhere without importing DatabaseModule
```

---

## Controllers

Controllers are **responsible for handling incoming HTTP requests and returning responses**. They define your API endpoints (routes). Controllers should be thin — they receive the request, call a service to do the actual work, and return the result.

```typescript
import {
  Controller, Get, Post, Put, Patch, Delete,
  Param, Body, Query, Headers, HttpCode, HttpStatus
} from "@nestjs/common";
import { UsersService } from "./users.service";
import { CreateUserDto } from "./dto/create-user.dto";
import { UpdateUserDto } from "./dto/update-user.dto";

@Controller("users")   // base route: /users
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  // GET /users
  @Get()
  findAll(@Query("page") page: string, @Query("limit") limit: string) {
    return this.usersService.findAll({ page: Number(page) || 1, limit: Number(limit) || 10 });
  }

  // GET /users/:id
  @Get(":id")
  findOne(@Param("id") id: string) {
    return this.usersService.findOne(id);
  }

  // POST /users
  @Post()
  @HttpCode(HttpStatus.CREATED)  // 201, this is also the default for POST
  create(@Body() createUserDto: CreateUserDto) {
    return this.usersService.create(createUserDto);
  }

  // PATCH /users/:id (partial update)
  @Patch(":id")
  update(@Param("id") id: string, @Body() updateUserDto: UpdateUserDto) {
    return this.usersService.update(id, updateUserDto);
  }

  // DELETE /users/:id
  @Delete(":id")
  @HttpCode(HttpStatus.NO_CONTENT)  // 204
  remove(@Param("id") id: string) {
    return this.usersService.remove(id);
  }

  // Access headers
  @Get("me/profile")
  getProfile(@Headers("authorization") authHeader: string) {
    return { authHeader };
  }
}
```

### Route Parameters and Wildcards

```typescript
@Controller("products")
export class ProductsController {
  // Nested routes
  @Get(":categoryId/items/:itemId")
  getItem(
    @Param("categoryId") categoryId: string,
    @Param("itemId") itemId: string
  ) {
    return { categoryId, itemId };
  }

  // Get ALL params as an object
  @Get(":id")
  findOne(@Param() params: { id: string }) {
    return { id: params.id };
  }

  // Wildcard routes
  @Get("search/*")
  search() {
    return "Matches /search/anything/here";
  }
}
```

---

## Providers and Services

Providers are the **backbone of NestJS's dependency injection system**. A service is the most common type of provider — it contains your business logic, database queries, and anything that is not directly related to handling HTTP requests.

```typescript
// users.service.ts
import { Injectable, NotFoundException } from "@nestjs/common";
import { InjectRepository } from "@nestjs/typeorm";
import { Repository } from "typeorm";
import { User } from "./entities/user.entity";
import { CreateUserDto } from "./dto/create-user.dto";
import { UpdateUserDto } from "./dto/update-user.dto";

@Injectable()  // marks this class as a provider that can be injected
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>,
  ) {}

  async findAll({ page, limit }: { page: number; limit: number }) {
    return this.usersRepository.find({
      skip: (page - 1) * limit,
      take: limit,
    });
  }

  async findOne(id: string) {
    const user = await this.usersRepository.findOne({ where: { id } });
    if (!user) {
      throw new NotFoundException(`User with ID ${id} not found`);
    }
    return user;
  }

  async create(createUserDto: CreateUserDto) {
    const user = this.usersRepository.create(createUserDto);
    return this.usersRepository.save(user);
  }

  async update(id: string, updateUserDto: UpdateUserDto) {
    const user = await this.findOne(id);  // throws if not found
    Object.assign(user, updateUserDto);
    return this.usersRepository.save(user);
  }

  async remove(id: string) {
    const user = await this.findOne(id);
    return this.usersRepository.remove(user);
  }
}
```

> **Interview Tip:** Keep controllers thin and services fat. The controller's job is ONLY to receive the request and call the right service method. All the actual logic (validation, business rules, database access) belongs in the service. This separation makes testing much easier.

---

## Dependency Injection

Dependency Injection (DI) means a class **does not create its own dependencies — they are provided (injected) from outside**. NestJS has a built-in DI container that handles creating and providing instances automatically.

```typescript
// Without DI — the class creates its own dependency (tightly coupled, hard to test)
class UsersService {
  private db = new DatabaseConnection();  // hard-coded dependency
}

// With DI — the dependency is INJECTED through the constructor
@Injectable()
export class UsersService {
  constructor(private readonly db: DatabaseConnection) {}
  // NestJS automatically creates and provides DatabaseConnection for us
}

@Module({
  providers: [UsersService, DatabaseConnection],  // register both
})
export class UsersModule {}
```

### Why DI matters

```typescript
// Because of DI, testing becomes easy — you can inject a FAKE version
describe("UsersService", () => {
  let service: UsersService;
  let mockRepo: Partial<Repository<User>>;

  beforeEach(async () => {
    mockRepo = {
      find: jest.fn().mockResolvedValue([{ id: "1", name: "Haseeb" }]),
      findOne: jest.fn(),
    };

    const module = await Test.createTestingModule({
      providers: [
        UsersService,
        { provide: getRepositoryToken(User), useValue: mockRepo },  // inject a fake repo
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
  });

  it("should return all users", async () => {
    const users = await service.findAll({ page: 1, limit: 10 });
    expect(users).toEqual([{ id: "1", name: "Haseeb" }]);
  });
});
```

### Provider Scopes

```typescript
import { Injectable, Scope } from "@nestjs/common";

// DEFAULT (Singleton) — one shared instance for the entire app (most common)
@Injectable()
export class UsersService {}

// REQUEST — new instance created for EVERY incoming request
@Injectable({ scope: Scope.REQUEST })
export class RequestScopedService {}

// TRANSIENT — new instance every time it is injected anywhere
@Injectable({ scope: Scope.TRANSIENT })
export class TransientService {}
```

### Custom Providers

```typescript
@Module({
  providers: [
    // Value provider
    { provide: "API_KEY", useValue: "abc123" },

    // Class provider (use a different class for the same token)
    { provide: PaymentService, useClass: StripePaymentService },

    // Factory provider (create the value dynamically)
    {
      provide: "DATABASE_CONNECTION",
      useFactory: async (configService: ConfigService) => {
        return createConnection(configService.get("DATABASE_URL"));
      },
      inject: [ConfigService],
    },
  ],
})
export class AppModule {}

// Injecting custom tokens
@Injectable()
export class SomeService {
  constructor(@Inject("API_KEY") private apiKey: string) {}
}
```

---

## Request Lifecycle

Understanding the order in which NestJS processes a request is a very common interview question.

```
Incoming Request
      ↓
1. Middleware            (runs first, like Express middleware)
      ↓
2. Guards                (authentication/authorization checks — can block the request)
      ↓
3. Interceptors (before) (runs before the route handler)
      ↓
4. Pipes                 (validate and transform incoming data)
      ↓
5. Route Handler         (your controller method actually runs)
      ↓
6. Interceptors (after)  (runs after the route handler, can transform the response)
      ↓
7. Exception Filters     (if anything threw an error, this catches it)
      ↓
Outgoing Response
```

> **Interview Tip:** This order is asked very often. The easy way to remember it: **Middleware → Guards → Interceptors (before) → Pipes → Handler → Interceptors (after) → Filters (only on error)**.

---

## DTOs and Validation

A DTO (Data Transfer Object) is a class that defines the **shape of data coming into your API**. Combined with `class-validator`, DTOs automatically validate incoming requests.

```bash
npm install class-validator class-transformer
```

```typescript
// dto/create-user.dto.ts
import {
  IsString, IsEmail, IsInt, Min, Max, MinLength, MaxLength,
  IsOptional, IsEnum, IsArray, ValidateNested, IsNotEmpty
} from "class-validator";
import { Type } from "class-transformer";

enum UserRole {
  ADMIN = "admin",
  USER = "user",
}

class AddressDto {
  @IsString()
  street: string;

  @IsString()
  city: string;
}

export class CreateUserDto {
  @IsString()
  @MinLength(2)
  @MaxLength(50)
  name: string;

  @IsEmail()
  email: string;

  @IsString()
  @MinLength(8, { message: "Password must be at least 8 characters" })
  password: string;

  @IsInt()
  @Min(18)
  @Max(120)
  @IsOptional()
  age?: number;

  @IsEnum(UserRole)
  @IsOptional()
  role?: UserRole = UserRole.USER;

  // Nested object validation
  @ValidateNested()
  @Type(() => AddressDto)
  @IsOptional()
  address?: AddressDto;

  // Array validation
  @IsArray()
  @IsString({ each: true })
  @IsOptional()
  tags?: string[];
}
```

```typescript
// dto/update-user.dto.ts — reuse CreateUserDto but make everything optional
import { PartialType } from "@nestjs/mapped-types";
import { CreateUserDto } from "./create-user.dto";

export class UpdateUserDto extends PartialType(CreateUserDto) {}
// This automatically makes all fields from CreateUserDto optional
```

```typescript
// Using the DTO in a controller — validation happens automatically
@Post()
create(@Body() createUserDto: CreateUserDto) {
  // If validation fails, NestJS automatically returns a 400 error
  // before this code even runs!
  return this.usersService.create(createUserDto);
}
```

---

## Pipes

Pipes have two main jobs: **transformation** (convert input data into the desired type) and **validation** (check if data is correct, throw an error if not).

```typescript
// Built-in pipes
import {
  ParseIntPipe, ParseBoolPipe, ParseUUIDPipe,
  ParseArrayPipe, DefaultValuePipe, ValidationPipe
} from "@nestjs/common";

@Controller("products")
export class ProductsController {
  // Converts string param to number automatically
  @Get(":id")
  findOne(@Param("id", ParseIntPipe) id: number) {
    return this.productsService.findOne(id);  // id is guaranteed to be a number
  }

  // Validate UUID format
  @Get(":id")
  findOne(@Param("id", ParseUUIDPipe) id: string) {
    return this.productsService.findOne(id);
  }

  // Query param with a default value
  @Get()
  findAll(@Query("limit", new DefaultValuePipe(10), ParseIntPipe) limit: number) {
    return this.productsService.findAll(limit);
  }
}
```

### Custom Pipe

```typescript
import { PipeTransform, Injectable, ArgumentMetadata, BadRequestException } from "@nestjs/common";

@Injectable()
export class TrimPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    if (typeof value === "string") {
      return value.trim();
    }
    if (typeof value === "object" && value !== null) {
      Object.keys(value).forEach(key => {
        if (typeof value[key] === "string") {
          value[key] = value[key].trim();
        }
      });
    }
    return value;
  }
}

// Custom validation pipe
@Injectable()
export class PositiveNumberPipe implements PipeTransform {
  transform(value: any) {
    const num = Number(value);
    if (isNaN(num) || num <= 0) {
      throw new BadRequestException("Value must be a positive number");
    }
    return num;
  }
}

// Using a custom pipe
@Get(":id")
findOne(@Param("id", PositiveNumberPipe) id: number) {
  return this.service.findOne(id);
}
```

### Global Validation Pipe (most common setup)

```typescript
// main.ts
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,             // strip properties NOT in the DTO
    forbidNonWhitelisted: true,  // throw error if extra properties are sent
    transform: true,             // automatically transform payloads to DTO class instances
    transformOptions: {
      enableImplicitConversion: true,  // auto-convert types like string "5" to number 5
    },
  }),
);
```

---

## Guards

Guards determine **whether a request is allowed to proceed**, usually for authentication and authorization. They run after middleware but before interceptors and pipes.

```typescript
// Basic guard structure
import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    const token = request.headers.authorization;
    return !!token;  // return true to allow, false to block (throws 403)
  }
}

// Using a guard on a specific route
@Get("profile")
@UseGuards(AuthGuard)
getProfile() {
  return "Protected data";
}

// Using a guard on an ENTIRE controller
@Controller("admin")
@UseGuards(AuthGuard)
export class AdminController {
  // every route here requires auth
}

// Using a guard GLOBALLY (in main.ts)
app.useGlobalGuards(new AuthGuard());
```

### JWT Auth Guard (real-world example)

```typescript
import { Injectable, ExecutionContext } from "@nestjs/common";
import { AuthGuard } from "@nestjs/passport";

@Injectable()
export class JwtAuthGuard extends AuthGuard("jwt") {
  // This uses the "jwt" Passport strategy automatically
  // Throws 401 if the token is missing or invalid
}

// Usage
@UseGuards(JwtAuthGuard)
@Get("profile")
getProfile(@Request() req) {
  return req.user;  // populated by the JWT strategy
}
```

### Role-Based Guard

```typescript
import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";
import { Reflector } from "@nestjs/core";

@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}

  canActivate(context: ExecutionContext): boolean {
    const requiredRoles = this.reflector.get<string[]>("roles", context.getHandler());
    if (!requiredRoles) return true;  // no roles required, allow

    const { user } = context.switchToHttp().getRequest();
    return requiredRoles.some(role => user.roles?.includes(role));
  }
}

// Used with a custom @Roles() decorator (see Custom Decorators section)
@UseGuards(JwtAuthGuard, RolesGuard)
@Roles("admin")
@Delete(":id")
remove(@Param("id") id: string) {
  return this.usersService.remove(id);
}
```

---

## Interceptors

Interceptors can **transform the response, log requests, add extra behavior before and after a route handler runs, or even completely intercept the result**. They wrap around the route handler.

```typescript
import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from "@nestjs/common";
import { Observable } from "rxjs";
import { map, tap } from "rxjs/operators";

// Logging interceptor
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest();
    console.log(`Before: ${request.method} ${request.url}`);

    const now = Date.now();
    return next.handle().pipe(
      tap(() => console.log(`After: ${Date.now() - now}ms`)),
    );
  }
}

// Transform interceptor (wraps ALL responses in a standard format)
@Injectable()
export class TransformInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next.handle().pipe(
      map(data => ({
        success: true,
        data,
        timestamp: new Date().toISOString(),
      })),
    );
  }
}
// A response like { id: 1, name: "Haseeb" }
// becomes { success: true, data: { id: 1, name: "Haseeb" }, timestamp: "..." }

// Caching interceptor
@Injectable()
export class CacheInterceptor implements NestInterceptor {
  private cache = new Map<string, any>();

  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest();
    const key = request.url;

    if (this.cache.has(key)) {
      return of(this.cache.get(key));  // return cached value, skip handler
    }

    return next.handle().pipe(
      tap(response => this.cache.set(key, response)),
    );
  }
}

// Using interceptors
@UseInterceptors(LoggingInterceptor)
@Get()
findAll() { }

// Globally
app.useGlobalInterceptors(new TransformInterceptor());
```

---

## Exception Filters

Exception filters **catch errors thrown anywhere in your application** and format the error response consistently.

```typescript
// NestJS has many built-in HTTP exceptions
import {
  BadRequestException, UnauthorizedException, ForbiddenException,
  NotFoundException, ConflictException, InternalServerErrorException
} from "@nestjs/common";

throw new NotFoundException("User not found");
throw new BadRequestException("Invalid input");
throw new ConflictException("Email already exists");
// Each automatically maps to the correct HTTP status code
```

### Custom Exception Filter

```typescript
import {
  ExceptionFilter, Catch, ArgumentsHost, HttpException, HttpStatus
} from "@nestjs/common";
import { Request, Response } from "express";

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();
    const status = exception.getStatus();

    response.status(status).json({
      statusCode: status,
      timestamp: new Date().toISOString(),
      path: request.url,
      message: exception.message,
    });
  }
}

// Catch ALL exceptions, including non-HTTP ones (like raw JS errors)
@Catch()
export class AllExceptionsFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();

    const status =
      exception instanceof HttpException
        ? exception.getStatus()
        : HttpStatus.INTERNAL_SERVER_ERROR;

    const message =
      exception instanceof HttpException
        ? exception.message
        : "Internal server error";

    response.status(status).json({
      statusCode: status,
      message,
      timestamp: new Date().toISOString(),
    });
  }
}

// Using a filter on a route
@UseFilters(HttpExceptionFilter)
@Get()
findAll() { }

// Globally (in main.ts)
app.useGlobalFilters(new AllExceptionsFilter());
```

### Custom Exception Class

```typescript
export class UserAlreadyExistsException extends HttpException {
  constructor(email: string) {
    super(`User with email ${email} already exists`, HttpStatus.CONFLICT);
  }
}

// Usage
if (existingUser) {
  throw new UserAlreadyExistsException(email);
}
```

---

## Middleware

Middleware is the **first thing that runs** when a request comes in, before guards, interceptors, or pipes. It has access to the raw request and response objects, similar to Express middleware.

```typescript
import { Injectable, NestMiddleware } from "@nestjs/common";
import { Request, Response, NextFunction } from "express";

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(`${req.method} ${req.originalUrl} - ${new Date().toISOString()}`);
    next();  // MUST call next() to continue to the next middleware/handler
  }
}
```

```typescript
// Applying middleware (done in the module, NOT with a decorator)
import { Module, NestModule, MiddlewareConsumer } from "@nestjs/common";

@Module({
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(LoggerMiddleware)
      .forRoutes("users");  // apply to all /users routes

      // More specific targeting:
      // .forRoutes({ path: "users", method: RequestMethod.GET })
      // .exclude("users/health")
  }
}

// Functional middleware (simpler, for basic cases)
export function logger(req: Request, res: Response, next: NextFunction) {
  console.log(`Request: ${req.method} ${req.url}`);
  next();
}

// Apply globally in main.ts
app.use(logger);
```

---

## Custom Decorators

NestJS lets you create your own decorators to keep code clean and reusable.

```typescript
// Custom parameter decorator — extract user from request
import { createParamDecorator, ExecutionContext } from "@nestjs/common";

export const CurrentUser = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;  // populated by an auth guard/strategy
  },
);

// Usage — much cleaner than manually accessing req.user every time
@Get("profile")
@UseGuards(JwtAuthGuard)
getProfile(@CurrentUser() user: User) {
  return user;
}

// Custom decorator with a specific property
export const CurrentUserId = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user?.id;
  },
);

getProfile(@CurrentUserId() userId: string) { }
```

### Metadata Decorator (used with Guards)

```typescript
import { SetMetadata } from "@nestjs/common";

// Custom @Roles() decorator
export const Roles = (...roles: string[]) => SetMetadata("roles", roles);

// Usage
@Roles("admin", "moderator")
@Delete(":id")
remove(@Param("id") id: string) {
  return this.usersService.remove(id);
}

// The RolesGuard (shown earlier) reads this metadata with Reflector
```

### Combining Decorators

```typescript
import { applyDecorators, UseGuards } from "@nestjs/common";

// Combine multiple decorators into one reusable decorator
export function Auth(...roles: string[]) {
  return applyDecorators(
    UseGuards(JwtAuthGuard, RolesGuard),
    Roles(...roles),
    ApiBearerAuth(),  // Swagger decorator
  );
}

// Usage — much cleaner!
@Auth("admin")
@Delete(":id")
remove(@Param("id") id: string) { }
```

---

## Database Integration (TypeORM)

TypeORM is one of the most common ORMs used with NestJS.

```bash
npm install @nestjs/typeorm typeorm pg
```

```typescript
// app.module.ts
import { TypeOrmModule } from "@nestjs/typeorm";

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: "postgres",
      host: process.env.DB_HOST,
      port: 5432,
      username: process.env.DB_USER,
      password: process.env.DB_PASSWORD,
      database: process.env.DB_NAME,
      entities: [__dirname + "/**/*.entity{.ts,.js}"],
      synchronize: false,  // use migrations in production instead!
    }),
  ],
})
export class AppModule {}
```

```typescript
// entities/user.entity.ts
import {
  Entity, PrimaryGeneratedColumn, Column, OneToMany,
  ManyToOne, CreateDateColumn, UpdateDateColumn, Index
} from "typeorm";
import { Post } from "../posts/entities/post.entity";

@Entity("users")
export class User {
  @PrimaryGeneratedColumn("uuid")
  id: string;

  @Column({ length: 100 })
  name: string;

  @Column({ unique: true })
  @Index()
  email: string;

  @Column({ select: false })  // never include in regular queries unless explicitly asked
  password: string;

  @Column({ default: "user" })
  role: string;

  @OneToMany(() => Post, post => post.author)
  posts: Post[];

  @CreateDateColumn()
  createdAt: Date;

  @UpdateDateColumn()
  updatedAt: Date;
}
```

### Using the Repository

```typescript
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>,
  ) {}

  // Find all
  findAll() {
    return this.usersRepository.find();
  }

  // Find with conditions
  findActive() {
    return this.usersRepository.find({ where: { status: "active" } });
  }

  // Find one
  findOne(id: string) {
    return this.usersRepository.findOne({ where: { id } });
  }

  // Find with relations (joins)
  findWithPosts(id: string) {
    return this.usersRepository.findOne({
      where: { id },
      relations: ["posts"],
    });
  }

  // Query builder (for complex queries)
  findWithFilters(search: string) {
    return this.usersRepository
      .createQueryBuilder("user")
      .where("user.name ILIKE :search", { search: `%${search}%` })
      .leftJoinAndSelect("user.posts", "post")
      .orderBy("user.createdAt", "DESC")
      .take(10)
      .getMany();
  }

  // Create
  async create(dto: CreateUserDto) {
    const user = this.usersRepository.create(dto);
    return this.usersRepository.save(user);
  }

  // Update
  async update(id: string, dto: UpdateUserDto) {
    await this.usersRepository.update(id, dto);
    return this.findOne(id);
  }

  // Delete
  remove(id: string) {
    return this.usersRepository.delete(id);
  }

  // Transactions
  async transferCredits(fromId: string, toId: string, amount: number) {
    return this.usersRepository.manager.transaction(async (manager) => {
      await manager.decrement(User, { id: fromId }, "credits", amount);
      await manager.increment(User, { id: toId }, "credits", amount);
    });
  }
}
```

---

## Database Integration (Prisma)

Prisma is a modern alternative to TypeORM, often praised for its type safety and developer experience.

```bash
npm install prisma @prisma/client
npx prisma init
```

```prisma
// schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(uuid())
  name      String
  email     String   @unique
  password  String
  posts     Post[]
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Post {
  id       String @id @default(uuid())
  title    String
  content  String
  author   User   @relation(fields: [authorId], references: [id])
  authorId String
}
```

```typescript
// prisma.service.ts
import { Injectable, OnModuleInit, OnModuleDestroy } from "@nestjs/common";
import { PrismaClient } from "@prisma/client";

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit, OnModuleDestroy {
  async onModuleInit() {
    await this.$connect();
  }

  async onModuleDestroy() {
    await this.$disconnect();
  }
}
```

```typescript
// users.service.ts
@Injectable()
export class UsersService {
  constructor(private prisma: PrismaService) {}

  findAll() {
    return this.prisma.user.findMany();
  }

  findOne(id: string) {
    return this.prisma.user.findUnique({ where: { id } });
  }

  findWithPosts(id: string) {
    return this.prisma.user.findUnique({
      where: { id },
      include: { posts: true },
    });
  }

  create(data: CreateUserDto) {
    return this.prisma.user.create({ data });
  }

  update(id: string, data: UpdateUserDto) {
    return this.prisma.user.update({ where: { id }, data });
  }

  remove(id: string) {
    return this.prisma.user.delete({ where: { id } });
  }
}
```

---

## Authentication with JWT

This is one of the most common things asked about in NestJS interviews.

```bash
npm install @nestjs/jwt @nestjs/passport passport passport-jwt bcrypt
```

```typescript
// auth/auth.service.ts
import { Injectable, UnauthorizedException } from "@nestjs/common";
import { JwtService } from "@nestjs/jwt";
import * as bcrypt from "bcrypt";
import { UsersService } from "../users/users.service";

@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService,
  ) {}

  async validateUser(email: string, password: string) {
    const user = await this.usersService.findByEmail(email);
    if (user && await bcrypt.compare(password, user.password)) {
      const { password, ...result } = user;  // strip password before returning
      return result;
    }
    return null;
  }

  async login(email: string, password: string) {
    const user = await this.validateUser(email, password);
    if (!user) {
      throw new UnauthorizedException("Invalid credentials");
    }

    const payload = { sub: user.id, email: user.email, roles: user.roles };

    return {
      access_token: this.jwtService.sign(payload),
      user,
    };
  }

  async register(createUserDto: CreateUserDto) {
    const hashedPassword = await bcrypt.hash(createUserDto.password, 10);
    return this.usersService.create({
      ...createUserDto,
      password: hashedPassword,
    });
  }
}
```

```typescript
// auth/strategies/jwt.strategy.ts
import { Injectable } from "@nestjs/common";
import { PassportStrategy } from "@nestjs/passport";
import { ExtractJwt, Strategy } from "passport-jwt";

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: process.env.JWT_SECRET,
    });
  }

  // Runs automatically AFTER the token is verified
  // Whatever you return here becomes req.user
  async validate(payload: any) {
    return { id: payload.sub, email: payload.email, roles: payload.roles };
  }
}
```

```typescript
// auth/auth.module.ts
import { Module } from "@nestjs/common";
import { JwtModule } from "@nestjs/jwt";
import { PassportModule } from "@nestjs/passport";
import { AuthService } from "./auth.service";
import { AuthController } from "./auth.controller";
import { JwtStrategy } from "./strategies/jwt.strategy";
import { UsersModule } from "../users/users.module";

@Module({
  imports: [
    UsersModule,
    PassportModule,
    JwtModule.register({
      secret: process.env.JWT_SECRET,
      signOptions: { expiresIn: "1d" },
    }),
  ],
  providers: [AuthService, JwtStrategy],
  controllers: [AuthController],
  exports: [AuthService],
})
export class AuthModule {}
```

```typescript
// auth/auth.controller.ts
import { Controller, Post, Body, UseGuards, Get, Request } from "@nestjs/common";
import { AuthService } from "./auth.service";
import { JwtAuthGuard } from "./guards/jwt-auth.guard";

@Controller("auth")
export class AuthController {
  constructor(private authService: AuthService) {}

  @Post("register")
  register(@Body() createUserDto: CreateUserDto) {
    return this.authService.register(createUserDto);
  }

  @Post("login")
  login(@Body() loginDto: { email: string; password: string }) {
    return this.authService.login(loginDto.email, loginDto.password);
  }

  @UseGuards(JwtAuthGuard)
  @Get("profile")
  getProfile(@Request() req) {
    return req.user;  // populated by the JwtStrategy
  }
}
```

---

## Authorization and Roles

```typescript
// roles.enum.ts
export enum Role {
  Admin = "admin",
  Manager = "manager",
  User = "user",
}

// roles.decorator.ts
import { SetMetadata } from "@nestjs/common";
import { Role } from "./roles.enum";

export const ROLES_KEY = "roles";
export const Roles = (...roles: Role[]) => SetMetadata(ROLES_KEY, roles);

// roles.guard.ts
import { Injectable, CanActivate, ExecutionContext } from "@nestjs/common";
import { Reflector } from "@nestjs/core";
import { ROLES_KEY } from "./roles.decorator";
import { Role } from "./roles.enum";

@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}

  canActivate(context: ExecutionContext): boolean {
    const requiredRoles = this.reflector.getAllAndOverride<Role[]>(ROLES_KEY, [
      context.getHandler(),
      context.getClass(),
    ]);

    if (!requiredRoles) return true;

    const { user } = context.switchToHttp().getRequest();
    return requiredRoles.some(role => user.roles?.includes(role));
  }
}

// Usage
@Controller("admin")
@UseGuards(JwtAuthGuard, RolesGuard)
export class AdminController {
  @Roles(Role.Admin)
  @Delete("users/:id")
  removeUser(@Param("id") id: string) {
    return this.usersService.remove(id);
  }

  @Roles(Role.Admin, Role.Manager)
  @Get("reports")
  getReports() {
    return this.reportsService.findAll();
  }
}
```

---

## Configuration Management

```bash
npm install @nestjs/config joi
```

```typescript
// config/configuration.ts
export default () => ({
  port: parseInt(process.env.PORT, 10) || 3000,
  database: {
    host: process.env.DB_HOST,
    port: parseInt(process.env.DB_PORT, 10) || 5432,
    name: process.env.DB_NAME,
  },
  jwt: {
    secret: process.env.JWT_SECRET,
    expiresIn: process.env.JWT_EXPIRES_IN || "1d",
  },
});
```

```typescript
// app.module.ts
import { ConfigModule } from "@nestjs/config";
import * as Joi from "joi";
import configuration from "./config/configuration";

@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true,           // available everywhere without re-importing
      load: [configuration],
      validationSchema: Joi.object({
        NODE_ENV: Joi.string().valid("development", "production", "test").default("development"),
        PORT: Joi.number().default(3000),
        DATABASE_URL: Joi.string().required(),
        JWT_SECRET: Joi.string().required(),
      }),
    }),
  ],
})
export class AppModule {}
```

```typescript
// Using ConfigService
import { ConfigService } from "@nestjs/config";

@Injectable()
export class SomeService {
  constructor(private configService: ConfigService) {}

  getJwtSecret() {
    return this.configService.get<string>("jwt.secret");
  }

  getPort() {
    return this.configService.get<number>("port");
  }
}
```

---

## Microservices

NestJS has built-in support for building microservices that communicate over TCP, Redis, RabbitMQ, Kafka, gRPC, and more.

```typescript
// main.ts — creating a microservice
import { NestFactory } from "@nestjs/core";
import { Transport, MicroserviceOptions } from "@nestjs/microservices";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.createMicroservice<MicroserviceOptions>(AppModule, {
    transport: Transport.TCP,
    options: { host: "localhost", port: 3001 },
  });
  await app.listen();
}
bootstrap();
```

```typescript
// Message pattern handler (receives messages, like an RPC endpoint)
import { Controller } from "@nestjs/common";
import { MessagePattern, Payload } from "@nestjs/microservices";

@Controller()
export class MathController {
  @MessagePattern("sum")
  sum(@Payload() data: number[]): number {
    return data.reduce((a, b) => a + b, 0);
  }
}
```

```typescript
// Calling a microservice from another service
import { ClientProxy } from "@nestjs/microservices";

@Injectable()
export class AppService {
  constructor(@Inject("MATH_SERVICE") private client: ClientProxy) {}

  async calculateSum(numbers: number[]) {
    return this.client.send("sum", numbers).toPromise();
  }
}
```

---

## WebSockets (Gateways)

NestJS Gateways let you build real-time features using WebSockets (built on Socket.io by default).

```bash
npm install @nestjs/websockets @nestjs/platform-socket.io
```

```typescript
import {
  WebSocketGateway, WebSocketServer, SubscribeMessage,
  MessageBody, ConnectedSocket, OnGatewayConnection, OnGatewayDisconnect
} from "@nestjs/websockets";
import { Server, Socket } from "socket.io";

@WebSocketGateway({ cors: true })
export class ChatGateway implements OnGatewayConnection, OnGatewayDisconnect {
  @WebSocketServer()
  server: Server;

  handleConnection(client: Socket) {
    console.log(`Client connected: ${client.id}`);
  }

  handleDisconnect(client: Socket) {
    console.log(`Client disconnected: ${client.id}`);
  }

  // Listens for "message" events from clients
  @SubscribeMessage("message")
  handleMessage(
    @MessageBody() data: { text: string; room: string },
    @ConnectedSocket() client: Socket,
  ) {
    // Broadcast to everyone in the room
    this.server.to(data.room).emit("message", data);
  }

  @SubscribeMessage("joinRoom")
  handleJoinRoom(
    @MessageBody() room: string,
    @ConnectedSocket() client: Socket,
  ) {
    client.join(room);
    client.emit("joinedRoom", room);
  }
}
```

---

## GraphQL in NestJS

```bash
npm install @nestjs/graphql @nestjs/apollo @apollo/server graphql
```

```typescript
// app.module.ts
import { GraphQLModule } from "@nestjs/graphql";
import { ApolloDriver, ApolloDriverConfig } from "@nestjs/apollo";

@Module({
  imports: [
    GraphQLModule.forRoot<ApolloDriverConfig>({
      driver: ApolloDriver,
      autoSchemaFile: true,  // generates schema.gql automatically from code
    }),
  ],
})
export class AppModule {}
```

```typescript
// users/entities/user.entity.ts (with GraphQL decorators)
import { ObjectType, Field, ID } from "@nestjs/graphql";

@ObjectType()
export class User {
  @Field(() => ID)
  id: string;

  @Field()
  name: string;

  @Field()
  email: string;
}
```

```typescript
// users/users.resolver.ts
import { Resolver, Query, Mutation, Args } from "@nestjs/graphql";
import { User } from "./entities/user.entity";
import { CreateUserInput } from "./dto/create-user.input";

@Resolver(() => User)
export class UsersResolver {
  constructor(private usersService: UsersService) {}

  @Query(() => [User])
  users() {
    return this.usersService.findAll();
  }

  @Query(() => User)
  user(@Args("id") id: string) {
    return this.usersService.findOne(id);
  }

  @Mutation(() => User)
  createUser(@Args("input") input: CreateUserInput) {
    return this.usersService.create(input);
  }
}
```

---

## File Uploads

```typescript
import { Controller, Post, UseInterceptors, UploadedFile } from "@nestjs/common";
import { FileInterceptor } from "@nestjs/platform-express";
import { diskStorage } from "multer";

@Controller("upload")
export class UploadController {
  @Post()
  @UseInterceptors(
    FileInterceptor("file", {
      storage: diskStorage({
        destination: "./uploads",
        filename: (req, file, cb) => {
          const uniqueName = `${Date.now()}-${file.originalname}`;
          cb(null, uniqueName);
        },
      }),
      limits: { fileSize: 5 * 1024 * 1024 },  // 5MB limit
      fileFilter: (req, file, cb) => {
        if (!file.mimetype.match(/\/(jpg|jpeg|png|gif)$/)) {
          return cb(new BadRequestException("Only image files allowed"), false);
        }
        cb(null, true);
      },
    }),
  )
  uploadFile(@UploadedFile() file: Express.Multer.File) {
    return {
      filename: file.filename,
      path: file.path,
      size: file.size,
    };
  }
}
```

---

## Caching

```bash
npm install @nestjs/cache-manager cache-manager
```

```typescript
// app.module.ts
import { CacheModule } from "@nestjs/cache-manager";

@Module({
  imports: [
    CacheModule.register({
      ttl: 60,    // seconds
      max: 100,   // max number of items in cache
      isGlobal: true,
    }),
  ],
})
export class AppModule {}
```

```typescript
// Using cache in a service
import { Inject } from "@nestjs/common";
import { CACHE_MANAGER } from "@nestjs/cache-manager";
import { Cache } from "cache-manager";

@Injectable()
export class ProductsService {
  constructor(@Inject(CACHE_MANAGER) private cacheManager: Cache) {}

  async findAll() {
    const cached = await this.cacheManager.get("products");
    if (cached) return cached;

    const products = await this.productsRepository.find();
    await this.cacheManager.set("products", products, 60);  // cache for 60s
    return products;
  }
}

// Or use the built-in interceptor (caches GET responses automatically)
import { CacheInterceptor, CacheTTL } from "@nestjs/cache-manager";

@UseInterceptors(CacheInterceptor)
@CacheTTL(30)
@Get()
findAll() {
  return this.productsService.findAll();
}
```

---

## Task Scheduling (Cron Jobs)

```bash
npm install @nestjs/schedule
```

```typescript
// app.module.ts
import { ScheduleModule } from "@nestjs/schedule";

@Module({
  imports: [ScheduleModule.forRoot()],
})
export class AppModule {}
```

```typescript
// tasks.service.ts
import { Injectable } from "@nestjs/common";
import { Cron, CronExpression, Interval, Timeout } from "@nestjs/schedule";

@Injectable()
export class TasksService {
  // Runs every day at midnight
  @Cron(CronExpression.EVERY_DAY_AT_MIDNIGHT)
  handleDailyCleanup() {
    console.log("Running daily cleanup...");
  }

  // Custom cron expression (every Monday at 9am)
  @Cron("0 9 * * 1")
  handleWeeklyReport() {
    console.log("Generating weekly report...");
  }

  // Runs every 10 seconds
  @Interval(10000)
  handlePolling() {
    console.log("Polling for updates...");
  }

  // Runs once, 5 seconds after the app starts
  @Timeout(5000)
  handleStartupTask() {
    console.log("Startup task running...");
  }
}
```

---

## Testing in NestJS

NestJS comes with Jest built-in and a testing module that mimics dependency injection.

```typescript
// users.service.spec.ts — Unit test
import { Test, TestingModule } from "@nestjs/testing";
import { getRepositoryToken } from "@nestjs/typeorm";
import { UsersService } from "./users.service";
import { User } from "./entities/user.entity";

describe("UsersService", () => {
  let service: UsersService;
  let repository: Repository<User>;

  const mockRepository = {
    find: jest.fn(),
    findOne: jest.fn(),
    create: jest.fn(),
    save: jest.fn(),
    remove: jest.fn(),
  };

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        UsersService,
        { provide: getRepositoryToken(User), useValue: mockRepository },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
    repository = module.get<Repository<User>>(getRepositoryToken(User));
  });

  it("should be defined", () => {
    expect(service).toBeDefined();
  });

  it("should return all users", async () => {
    const result = [{ id: "1", name: "Haseeb" }];
    mockRepository.find.mockResolvedValue(result);

    expect(await service.findAll({ page: 1, limit: 10 })).toEqual(result);
  });

  it("should throw NotFoundException when user does not exist", async () => {
    mockRepository.findOne.mockResolvedValue(null);

    await expect(service.findOne("999")).rejects.toThrow(NotFoundException);
  });
});
```

```typescript
// users.controller.spec.ts — Controller test
describe("UsersController", () => {
  let controller: UsersController;
  let service: UsersService;

  const mockUsersService = {
    findAll: jest.fn(),
    findOne: jest.fn(),
    create: jest.fn(),
  };

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [{ provide: UsersService, useValue: mockUsersService }],
    }).compile();

    controller = module.get<UsersController>(UsersController);
    service = module.get<UsersService>(UsersService);
  });

  it("should create a user", async () => {
    const dto = { name: "Haseeb", email: "h@test.com", password: "password123" };
    const result = { id: "1", ...dto };
    mockUsersService.create.mockResolvedValue(result);

    expect(await controller.create(dto)).toEqual(result);
    expect(service.create).toHaveBeenCalledWith(dto);
  });
});
```

```typescript
// app.e2e-spec.ts — End-to-end test (tests the full HTTP request/response cycle)
import { Test, TestingModule } from "@nestjs/testing";
import { INestApplication } from "@nestjs/common";
import * as request from "supertest";
import { AppModule } from "../src/app.module";

describe("UsersController (e2e)", () => {
  let app: INestApplication;

  beforeAll(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it("/users (GET)", () => {
    return request(app.getHttpServer())
      .get("/users")
      .expect(200)
      .expect(res => {
        expect(Array.isArray(res.body)).toBe(true);
      });
  });

  it("/users (POST) creates a user", () => {
    return request(app.getHttpServer())
      .post("/users")
      .send({ name: "Haseeb", email: "h@test.com", password: "password123" })
      .expect(201);
  });

  afterAll(async () => {
    await app.close();
  });
});
```

---

## Swagger / API Documentation

```bash
npm install @nestjs/swagger
```

```typescript
// main.ts
import { SwaggerModule, DocumentBuilder } from "@nestjs/swagger";

const config = new DocumentBuilder()
  .setTitle("My API")
  .setDescription("API documentation for my app")
  .setVersion("1.0")
  .addBearerAuth()
  .build();

const document = SwaggerModule.createDocument(app, config);
SwaggerModule.setup("api-docs", app, document);
// Now visit http://localhost:3000/api-docs to see interactive API docs
```

```typescript
// Documenting DTOs
import { ApiProperty } from "@nestjs/swagger";

export class CreateUserDto {
  @ApiProperty({ example: "Haseeb Javed", description: "Full name of the user" })
  name: string;

  @ApiProperty({ example: "haseeb@example.com" })
  email: string;

  @ApiProperty({ minLength: 8 })
  password: string;
}

// Documenting controllers
import { ApiTags, ApiOperation, ApiResponse, ApiBearerAuth } from "@nestjs/swagger";

@ApiTags("users")
@Controller("users")
export class UsersController {
  @ApiOperation({ summary: "Get all users" })
  @ApiResponse({ status: 200, description: "List of users returned successfully" })
  @Get()
  findAll() { }

  @ApiBearerAuth()
  @ApiOperation({ summary: "Create a new user" })
  @ApiResponse({ status: 201, description: "User created" })
  @ApiResponse({ status: 400, description: "Validation failed" })
  @Post()
  create(@Body() dto: CreateUserDto) { }
}
```

---

## Logging

```typescript
import { Injectable, Logger } from "@nestjs/common";

@Injectable()
export class UsersService {
  private readonly logger = new Logger(UsersService.name);

  async create(dto: CreateUserDto) {
    this.logger.log(`Creating user with email: ${dto.email}`);
    try {
      const user = await this.usersRepository.save(dto);
      this.logger.log(`User created successfully: ${user.id}`);
      return user;
    } catch (error) {
      this.logger.error(`Failed to create user: ${error.message}`, error.stack);
      throw error;
    }
  }
}

// Logger methods
this.logger.log("Info message");
this.logger.error("Error message", "stack trace");
this.logger.warn("Warning message");
this.logger.debug("Debug message");
this.logger.verbose("Verbose message");
```

---

## Best Practices

```typescript
// 1. Keep controllers thin — push logic into services
// 2. Use DTOs for ALL incoming data, never trust raw request bodies
// 3. Always use the global ValidationPipe with whitelist: true
// 4. Use environment variables for secrets, never hardcode them
// 5. Use guards for auth, not manual checks scattered in controllers
// 6. Use exception filters for consistent error response format
// 7. Never use synchronize: true in production (TypeORM) — use migrations
// 8. Write unit tests for services, e2e tests for full request flows
// 9. Use interfaces/DTOs to define clear contracts between layers
// 10. Organize code by FEATURE (users/, products/) not by TYPE (controllers/, services/)

// Good structure (feature-based)
src/
  users/
    users.controller.ts
    users.service.ts
    users.module.ts

// Avoid (type-based, gets messy fast)
src/
  controllers/
    users.controller.ts
  services/
    users.service.ts
```

---

## Common Interview Questions

### Q1. What is NestJS and why would you choose it over plain Express?
NestJS is a TypeScript-first Node.js framework that brings a structured, modular architecture inspired by Angular. While Express gives you flexibility but no built-in structure, NestJS provides dependency injection, decorators, and clear separation of concerns (controllers, services, modules) out of the box. This makes it much easier to build, test, and maintain large applications, especially with bigger teams.

### Q2. What is the request lifecycle in NestJS?
A request flows through these stages in order: Middleware, then Guards (auth checks), then Interceptors (before the handler), then Pipes (validation/transformation), then the route handler itself, then Interceptors again (after the handler, can transform the response), and finally Exception Filters if any error was thrown along the way.

### Q3. What is Dependency Injection and how does NestJS implement it?
Dependency Injection is a pattern where a class receives its dependencies from an outside source instead of creating them itself. NestJS has a built-in IoC (Inversion of Control) container that automatically creates and provides instances of classes marked with `@Injectable()` wherever they are needed, usually through the constructor. This makes testing much easier because you can inject mock dependencies instead of real ones.

### Q4. What is the difference between a Guard and a Middleware?
Both run before the route handler, but Middleware runs first and has access to the raw request/response (like Express middleware), with no knowledge of which specific route handler will run. Guards run after middleware and have full execution context, including knowledge of the route handler and any metadata attached via decorators — making them ideal for authentication and authorization checks that decide whether the request should continue.

### Q5. What is the purpose of a Pipe in NestJS?
A pipe transforms or validates incoming data before it reaches the route handler. NestJS has built-in pipes like `ParseIntPipe` (converts a string param to a number) and `ValidationPipe` (validates a DTO using class-validator decorators). If validation fails, the pipe throws an exception and the request never reaches your controller logic.

### Q6. What is a DTO and why is it important?
A DTO (Data Transfer Object) is a class that defines the expected shape of incoming data, usually for a request body. Combined with `class-validator` decorators and NestJS's `ValidationPipe`, DTOs let you automatically validate and reject malformed requests before your business logic even runs, which keeps your controllers and services clean and your API safe from bad input.

### Q7. What is the difference between a Guard and an Interceptor?
Guards decide whether a request is ALLOWED to proceed at all (returning true or false) — they run early and can block requests entirely with a 403 error. Interceptors wrap around the entire request, running logic both before AND after the handler, and they can transform the response data, add logging, or even replace the result of the handler entirely. Guards answer "should this happen?" while interceptors answer "what extra behavior wraps around this?"

### Q8. How do you handle errors globally in NestJS?
You create a class that implements `ExceptionFilter`, decorate it with `@Catch()` (optionally specifying which exception types to catch), and register it globally with `app.useGlobalFilters()` in `main.ts`. This lets you format every error response consistently across your whole application, regardless of where in the code the error was thrown.

### Q9. What are the differences between provider scopes in NestJS?
The default scope is Singleton, meaning one shared instance exists for the entire application lifetime. Request scope creates a brand new instance for every incoming request, which is useful when you need per-request state but adds some performance overhead. Transient scope creates a new instance every single time the provider is injected anywhere, even within the same request.

### Q10. How does NestJS handle authentication with JWT?
NestJS typically uses Passport with the `passport-jwt` strategy. You create a `JwtStrategy` that extracts and verifies the token from the request, and whatever you return from its `validate()` method becomes `request.user`. You protect routes with a `JwtAuthGuard` that wraps this strategy, and you can combine it with a `RolesGuard` for authorization checks afterward.

### Q11. What is the difference between `@Injectable()` and `@Controller()`?
`@Injectable()` marks a class as a provider that can be injected into other classes via NestJS's dependency injection system — typically used for services. `@Controller()` marks a class as responsible for handling incoming HTTP requests and defining routes. Controllers can inject providers (services) through their constructor, but providers are not meant to handle HTTP requests directly.

### Q12. How would you structure a large NestJS application?
The recommended approach is feature-based modules — group all related files (controller, service, module, DTOs, entities) together by feature, like a `users/` folder containing everything related to users, rather than splitting by file type into `controllers/`, `services/`, etc. Shared, cross-cutting code like decorators, guards, and pipes used across many features goes into a `common/` folder.

### Q13. What is the difference between TypeORM and Prisma in a NestJS app?
TypeORM uses an Active Record or Data Mapper pattern with decorator-based entity classes and integrates very tightly with NestJS through `@nestjs/typeorm`. Prisma uses a separate schema file (`schema.prisma`) to define your data model and generates a fully type-safe client based on it. Many developers find Prisma's developer experience, autocomplete, and migrations cleaner, while TypeORM feels more native to the NestJS decorator-based style.

### Q14. How do you implement role-based access control (RBAC) in NestJS?
You create a custom `@Roles()` decorator using `SetMetadata` to attach required roles to a route handler. Then you create a `RolesGuard` that reads this metadata using `Reflector` and compares it against the roles attached to the authenticated user (usually populated by a JWT strategy). You apply both the authentication guard and the roles guard together using `@UseGuards(JwtAuthGuard, RolesGuard)`.

### Q15. What is the difference between unit tests and e2e tests in NestJS?
Unit tests check individual pieces of code in isolation, like a single service method, using NestJS's `Test.createTestingModule()` with mocked dependencies (such as a mocked repository) so the database is never actually touched. End-to-end (e2e) tests check the full request/response cycle by spinning up the actual NestJS application and making real HTTP requests using a library like `supertest`, verifying the whole system works together correctly.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Next.js, TypeScript, NestJS, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).