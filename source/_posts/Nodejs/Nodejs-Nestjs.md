---
title: Node.js - Nest.js framework
tags:
  - Backend
  - Node.js
categories:
  - [Node.js, Nest.js]
date: 2021-07-01
---
# Nest.js framework
* Currently, it supports two libraries — Express and Fastify
* it forces developers to use a specific architecture by introducing **Angular-like modules, services, and controllers**, ensuring the application is scalable, highly testable, and loosely coupled
* A controller is a class annotated with the `@Controller` decorator and it checks what request comes in and calls the appropriate service’s method. They don’t care about what’s going on between the request and the response.
* A service is a class annotated with the @Injectable decorator. It contains domain (business) logic. By separating the access layer (controllers) and logic layer (services), we have a clear separation of concerns.
* **Dependency injection is one of the most important aspects of Nest**. By providing the support out of the box, Nest allows us to write **loosely coupled code**, which, in turn, is also **easily testable**.
* By using dependency injection, it is very easy to mock out the modules we are not currently testing thanks to Nest’s *custom providers* feature.
* Nest stays on top of the new trends and makes it very easy to write an application based on the microservices architecture.
* Nest is used for building REST APIs but also the architecture can be used to create a GraphQL API as well.

## Sample Controller
### Sample 1
```js
@Controller('cats')
export class CatsController {
  @Post()
  create(@Body() createCatDto: CreateCatDto) {
    return 'This action adds a new cat';
  }

  @Get()
  findAll(@Query() query: ListAllEntities) {
    return `This action returns all cats (limit: ${query.limit} items)`;
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return `This action returns a #${id} cat`;
  }

  @Put(':id')
  update(@Param('id') id: string, @Body() updateCatDto: UpdateCatDto) {
    return `This action updates a #${id} cat`;
  }

  @Delete(':id')
  remove(@Param('id') id: string) {
    return `This action removes a #${id} cat`;
  }
}
```
### Sample 2
```js
@Controller('cats')
export class CatsController {
  constructor(private readonly catsService: CatsService) {}

  @Post()
  async create(@Body() createCatDto: CreateCatDto) {
    this.catsService.create(createCatDto);
  }

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

## Sample Service
```js
@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}
```

## Sources
* [Take your Node backend to the next level with NestJS](https://blog.logrocket.com/node-back-end-next-level-nestjs/)