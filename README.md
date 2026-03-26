<div dir="rtl">

## دوره جامع تست‌نویسی در NestJS



[![HitCount](https://hits.dwyl.com/irzix/nestjs-testing-course.svg?style=flat-square)](https://hits.dwyl.com/irzix/nestjs-testing-course)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Alireza%20Mohaqeqi-0A66C2?logo=linkedin)](https://www.linkedin.com/in/alirezamohaqeqi/)
[![GitHub](https://img.shields.io/badge/GitHub-irzix%2Fnestjs--testing--course-blue?logo=github)](https://github.com/irzix/nestjs-testing-course/)

---

## فهرست مطالب

- [چرا تست‌نویسی مهم است؟](#چرا-تستنویسی-مهم-است)
- [راه‌اندازی](#راهاندازی)
  - [ساختار فایل‌های تست](#ساختار-فایلهای-تست)
  - [دستورات اجرای تست](#دستورات-اجرای-تست)
- [سطح ۱ — مبانی Jest](#سطح-۱-مبانی-jest)
  - [ساختار اصلی یک تست](#ساختار-اصلی-یک-تست)
  - [Matchers اصلی Jest](#matchers-اصلی-jest)
  - [چرخه حیات تست — Lifecycle Hooks](#چرخه-حیات-تست-lifecycle-hooks)
  - [Skip و Only](#skip-و-only)
- [سطح ۲ — Unit Testing](#سطح-۲-unit-testing)
  - [مفهوم Mock](#مفهوم-mock)
  - [اولین Unit Test — تست Service](#اولین-unit-test-تست-service)
  - [jest.fn() — قدرت Mocking](#jestfn-قدرت-mocking)
  - [jest.spyOn — جاسوسی روی متدها](#jestspyon-جاسوسی-روی-متدها)
  - [تست Controller](#تست-controller)
- [سطح ۳ — Integration / E2E Testing](#سطح-۳-integration-e2e-testing)
  - [تنظیمات E2E](#تنظیمات-e2e)
  - [اولین E2E Test](#اولین-e2e-test)
  - [Authentication در E2E Tests](#authentication-در-e2e-tests)
- [سطح ۴ — تکنیک‌های پیشرفته](#سطح-۴-تکنیکهای-پیشرفته)
  - [TDD — Test Driven Development](#tdd-test-driven-development)
  - [تست Guards](#تست-guards)
  - [تست Pipes](#تست-pipes)
  - [تست Interceptors](#تست-interceptors)
  - [Faker.js — دیتای تستی واقع‌گرایانه](#fakerjs-دیتای-تستی-واقعگرایانه)
  - [Test Coverage — تحلیل پوشش کد](#test-coverage-تحلیل-پوشش-کد)
- [TestContainers — دیتابیس واقعی در تست](#testcontainers-دیتابیس-واقعی-در-تست)
- [سطح ۵ — تکنیک‌های تکمیلی](#سطح-۵-تکنیکهای-تکمیلی)
  - [تست با دیتابیس In-Memory (SQLite)](#تست-با-دیتابیس-in-memory-sqlite)
  - [تست Exception Filters](#تست-exception-filters)
  - [Mock کامل ماژول با jest.mock()](#mock-کامل-ماژول-با-jestmock)
  - [تست با ConfigService و متغیرهای محیطی](#تست-با-configservice-و-متغیرهای-محیطی)
  - [تست Middleware](#تست-middleware)
  - [تست Event و Queue با BullMQ](#تست-event-و-queue-با-bullmq)
  - [Database Seeding و Factory Pattern پیشرفته](#database-seeding-و-factory-pattern-پیشرفته)
  - [تست Cron Jobs با nestjs/schedule@](#تست-cron-jobs-با-nestjsschedule)
  - [Mock کردن Third-Party Services](#mock-کردن-third-party-services)
  - [CI/CD Integration با GitHub Actions](#cicd-integration-با-github-actions)
- [سطح ۶ — عمق بیشتر](#سطح-۶-عمق-بیشتر)
  - [useValue vs useFactory vs useClass در TestingModule](#usevalue-vs-usefactory-vs-useclass-در-testingmodule)
  - [Supertest پیشرفته — Headers، Cookies و فایل‌ها](#supertest-پیشرفته-headers-cookies-و-فایلها)
  - [Snapshot Testing](#snapshot-testing)
  - [تست WebSocket Gateway](#تست-websocket-gateway)
- [بهترین شیوه‌ها و نکات کلیدی](#بهترین-شیوهها-و-نکات-کلیدی)
- [جدول مقایسه انواع تست](#جدول-مقایسه-انواع-تست)
- [Cheat Sheet — مرجع سریع](#cheat-sheet-مرجع-سریع)

---

## چرا تست‌نویسی مهم است؟

در دنیای توسعه نرم‌افزار حرفه‌ای، تست‌نویسی دیگر یک «گزینه» نیست، بلکه یک «الزام» است. فکر کنید یک پروژه بزرگ دارید که ده‌ها سرویس و صدها متد دارد. بدون تست، هر بار که کدی تغییر می‌کنید، نگران این هستید که «مبادا چیزی شکسته باشد». با تست‌نویسی، این اطمینان را دارید.

تست‌نویسی مزایای متعددی دارد:

- شناسایی باگ‌ها قبل از رسیدن به Production
- اطمینان از اینکه تغییرات جدید چیزی را نمی‌شکنند (Regression Testing)
- مستندسازی خودکار رفتار کد
- طراحی بهتر کد (کدی که قابل تست است، معمولاً بهتر طراحی شده)
- اعتماد بیشتر هنگام Refactoring

> 💡 **NestJS و Testing** — NestJS به صورت داخلی از Jest پشتیبانی می‌کند و همه چیز آماده است. وقتی یک پروژه جدید با CLI می‌سازید، فایل‌های تست و تنظیمات Jest از قبل وجود دارند.

---

## راه‌اندازی

اول از همه باید NestJS CLI را نصب کنید و یک پروژه جدید بسازید:

```bash
# نصب NestJS CLI
npm install -g @nestjs/cli

# ساخت پروژه جدید
nest new nestjs-testing-course

# ورود به پوشه پروژه
cd nestjs-testing-course

# نصب پکیج‌های مورد نیاز برای تست
npm install --save-dev @nestjs/testing supertest
npm install --save-dev @types/supertest

# نصب ابزارهای اضافه
npm install --save-dev @faker-js/faker
```

</div>

<div dir="rtl">

### ساختار فایل‌های تست

NestJS برای هر ماژول دو نوع فایل تست می‌سازد:

- فایل‌های `*.spec.ts`: برای Unit Test
- فایل‌های `test/*.e2e-spec.ts`: برای E2E Test

```
src/
  users/
    users.controller.ts
    users.service.ts
    users.controller.spec.ts   ← Unit test for Controller
    users.service.spec.ts      ← Unit test for Service
test/
  app.e2e-spec.ts              ← E2E tests
  jest-e2e.json                ← E2E Jest config
jest.config.js                 ← Main Jest config
```

### دستورات اجرای تست

```bash
# اجرای همه تست‌های Unit
npm run test

# اجرای تست‌ها در حالت Watch (اجرا با هر تغییر)
npm run test:watch

# اجرای تست‌ها با نمایش Coverage
npm run test:cov

# اجرای تست‌های E2E
npm run test:e2e

# اجرای یک فایل تست خاص
npx jest users.service.spec.ts

# اجرای تست‌هایی که نامشان با keyword مطابقت دارد
npx jest --testNamePattern="should create user"
```

---

## سطح ۱ — مبانی Jest

### ساختار اصلی یک تست

هر تست در Jest از سه بخش اصلی تشکیل شده است:

```typescript
// ساختار اصلی
describe('نام گروه تست', () => {
  it('توضیح این تست چیست', () => {
    // Arrange: آماده‌سازی
    const input = 5;

    // Act: اجرا
    const result = input * 2;

    // Assert: بررسی نتیجه
    expect(result).toBe(10);
  });
});
```

> 💡 **الگوی AAA** — همیشه سعی کنید تست‌هایتان از سه مرحله Arrange, Act, Assert پیروی کنند. این الگو تست‌ها را خواناتر و قابل نگهداری‌تر می‌کند.

### Matchers اصلی Jest

#### بررسی مقادیر ساده

```typescript
describe('Matchers اصلی', () => {

  // toBe: برای مقادیر primitive (number, string, boolean)
  // از === استفاده می‌کند
  it('بررسی مقادیر ساده با toBe', () => {
    expect(2 + 2).toBe(4);
    expect('hello').toBe('hello');
    expect(true).toBe(true);
  });

  // toEqual: برای object و array - مقدار را مقایسه می‌کند نه reference را
  it('بررسی object با toEqual', () => {
    const user = { name: 'Ali', age: 25 };
    expect(user).toEqual({ name: 'Ali', age: 25 }); // ✓
    // expect(user).toBe({ name: 'Ali', age: 25 }); // ✗ fail می‌شود!
  });

  // toStrictEqual: مانند toEqual ولی undefined properties هم بررسی می‌کند
  it('تفاوت toEqual و toStrictEqual', () => {
    class User { name: string; constructor(n: string) { this.name = n; } }
    expect(new User('Ali')).toEqual({ name: 'Ali' });        // ✓
    // expect(new User('Ali')).toStrictEqual({ name: 'Ali' }); // ✗
  });
});
```

#### بررسی Truthiness

```typescript
describe('Truthiness Matchers', () => {
  it('بررسی null و undefined', () => {
    expect(null).toBeNull();
    expect(undefined).toBeUndefined();
    expect('value').toBeDefined();
  });

  it('بررسی truthy/falsy', () => {
    expect(1).toBeTruthy();      // هر چیزی که در if، true تلقی شود
    expect(0).toBeFalsy();       // هر چیزی که در if، false تلقی شود
    expect('').toBeFalsy();
    expect([]).toBeTruthy();     // آرایه خالی truthy است!
  });
});
```

</div>

<div dir="rtl">

#### بررسی اعداد

```typescript
describe('Number Matchers', () => {
  it('مقایسه اعداد', () => {
    expect(10).toBeGreaterThan(5);
    expect(10).toBeGreaterThanOrEqual(10);
    expect(5).toBeLessThan(10);
    expect(5).toBeLessThanOrEqual(5);
  });

  it('اعداد اعشاری - از toBeCloseTo استفاده کنید', () => {
    // 0.1 + 0.2 = 0.30000000000000004 در JavaScript!
    expect(0.1 + 0.2).not.toBe(0.3);                 // ✓
    expect(0.1 + 0.2).toBeCloseTo(0.3, 5);           // ✓ با 5 رقم اعشار
  });
});
```

#### بررسی رشته‌ها

```typescript
describe('String Matchers', () => {
  it('بررسی با regex', () => {
    expect('hello world').toMatch(/world/);
    expect('hello world').toMatch('world');         // می‌توان string هم داد
    expect('test@example.com').toMatch(/^\w+@\w+\.\w+$/);
  });

  it('بررسی طول', () => {
    expect('hello').toHaveLength(5);
  });
});
```

#### بررسی آرایه‌ها

```typescript
describe('Array Matchers', () => {
  const fruits = ['apple', 'banana', 'cherry'];

  it('بررسی وجود عنصر', () => {
    expect(fruits).toContain('banana');
    expect(fruits).not.toContain('grape');
  });

  it('بررسی طول آرایه', () => {
    expect(fruits).toHaveLength(3);
  });

  it('بررسی آرایه‌ای از objectها', () => {
    const users = [{ name: 'Ali' }, { name: 'Sara' }];
    expect(users).toContainEqual({ name: 'Ali' });
  });
});
```

#### بررسی Exception

```typescript
describe('Exception Matchers', () => {
  function divide(a: number, b: number): number {
    if (b === 0) throw new Error('Cannot divide by zero');
    return a / b;
  }

  it('بررسی throw شدن error', () => {
    // مهم: باید function را wrap کنید!
    expect(() => divide(10, 0)).toThrow();
    expect(() => divide(10, 0)).toThrow('Cannot divide by zero');
    expect(() => divide(10, 0)).toThrow(Error);
    expect(() => divide(10, 0)).toThrowError(/divide by zero/);
  });

  it('بررسی async error', async () => {
    async function fetchUser(id: number) {
      if (id <= 0) throw new Error('Invalid ID');
    }
    await expect(fetchUser(-1)).rejects.toThrow('Invalid ID');
  });
});
```

### چرخه حیات تست — Lifecycle Hooks

Jest چهار hook اصلی دارد که به شما امکان می‌دهند کارهایی را قبل یا بعد از تست‌ها انجام دهید:

```typescript
describe('Lifecycle Hooks', () => {
  let database: any[];
  let counter: number;

  // یک بار قبل از همه تست‌های این describe اجرا می‌شود
  beforeAll(() => {
    console.log('شروع Suite تست');
    database = [];
    counter = 0;
  });

  // قبل از هر تست اجرا می‌شود
  beforeEach(() => {
    console.log('تست جدید شروع شد');
    counter++;
    database = [{ id: 1, name: 'Ali' }]; // reset می‌کنیم
  });

  // بعد از هر تست اجرا می‌شود
  afterEach(() => {
    console.log(`تست ${counter} تمام شد`);
    // cleanup اگر لازم باشد
  });

  // یک بار بعد از همه تست‌های این describe اجرا می‌شود
  afterAll(() => {
    console.log('✅ همه تست‌ها تمام شدند');
    database = null;
  });

  it('اول', () => {
    expect(database).toHaveLength(1);
    database.push({ id: 2, name: 'Sara' });
  });

  it('دوم - database دوباره یک عنصر دارد (reset شد)', () => {
    expect(database).toHaveLength(1); // چون beforeEach reset کرد
  });
});
```

> 💡 **ترتیب اجرای Hooks** — ترتیب اجرا: `beforeAll` ← `beforeEach` ← `[تست]` ← `afterEach` ← `afterAll`. اگر `describe` های تودرتو داشته باشید، هر کدام hook های مستقل دارند.

### Skip و Only

```typescript
describe('Skip و Only', () => {

  // it.skip: این تست را رد کن
  it.skip('این تست اجرا نمی‌شود', () => {
    expect(1).toBe(2); // fail می‌شد ولی skip شد
  });

  // xit معادل it.skip است
  xit('این هم رد می‌شود', () => {});

  // it.only: فقط این تست را اجرا کن (بقیه skip می‌شوند)
  it.only('فقط این تست اجرا می‌شود', () => {
    expect(1 + 1).toBe(2);
  });

  it('این تست skip می‌شود چون بالا only داریم', () => {
    expect(true).toBe(true);
  });

  // describe.skip: کل گروه را skip کن
  describe.skip('این گروه اجرا نمی‌شود', () => {
    it('test', () => {});
  });
});
```

> ⚠️ **هشدار** — هرگز `it.only` را در کد نهایی رها نکنید! این کار باعث می‌شود بقیه تست‌ها اجرا نشوند. از آن فقط برای debugging موقت استفاده کنید.

---

## سطح ۲ — Unit Testing

در این سطح یاد می‌گیریم چطور Service ها و کدهای business logic را به صورت ایزوله تست کنیم. «ایزوله» یعنی وابستگی‌ها (مثل دیتابیس) را Fake می‌کنیم.

### مفهوم Mock

Mock یک جایگزین تقلبی برای یک dependency واقعی است. وقتی یک Service را تست می‌کنیم، نمی‌خواهیم واقعاً به دیتابیس متصل شویم. پس یک Mock می‌سازیم که رفتار دیتابیس را شبیه‌سازی می‌کند.

```typescript
// سه نوع اصلی Test Double:

// ۱. Stub: همیشه یک مقدار ثابت برمی‌گرداند
const userRepositoryStub = {
  findOne: jest.fn().mockResolvedValue({ id: 1, name: 'Ali' })
};

// ۲. Mock: علاوه بر stub، تعداد صدا زده شدن را هم بررسی می‌کند
const emailServiceMock = {
  sendEmail: jest.fn()  // ما verify می‌کنیم که آیا صدا زده شده یا نه
};

// ۳. Spy: بر روی یک object واقعی 'جاسوسی' می‌کند
const realService = new UserService();
const spy = jest.spyOn(realService, 'findUser');
```

</div>

<div dir="rtl">

### اولین Unit Test — تست Service

#### سناریو: UserService

فرض کنید یک UserService داریم که با Repository کار می‌کند. می‌خواهیم آن را بدون نیاز به دیتابیس تست کنیم.

**`src/users/user.entity.ts`**

```typescript
export class User {
  id: number;
  name: string;
  email: string;
  age: number;
  isActive: boolean = true;
}
```

**`src/users/users.service.ts`**

```typescript
import { Injectable, NotFoundException, BadRequestException } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './user.entity';

@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private readonly userRepository: Repository<User>,
  ) {}

  async findAll(): Promise<User[]> {
    return this.userRepository.find();
  }

  async findOne(id: number): Promise<User> {
    const user = await this.userRepository.findOne({ where: { id } });
    if (!user) {
      throw new NotFoundException(`User with id ${id} not found`);
    }
    return user;
  }

  async create(data: Partial<User>): Promise<User> {
    if (!data.email || !data.name) {
      throw new BadRequestException('Name and email are required');
    }
    const user = this.userRepository.create(data);
    return this.userRepository.save(user);
  }

  async remove(id: number): Promise<void> {
    const user = await this.findOne(id);
    await this.userRepository.remove(user);
  }
}
```

**`src/users/users.service.spec.ts`** — فایل تست

```typescript
import { Test, TestingModule } from '@nestjs/testing';
import { getRepositoryToken } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { NotFoundException, BadRequestException } from '@nestjs/common';
import { UsersService } from './users.service';
import { User } from './user.entity';

// تعریف نوع Mock Repository
type MockRepository<T = any> = Partial<Record<keyof Repository<T>, jest.Mock>>;

// Factory function برای ساخت Mock Repository
const createMockRepository = <T = any>(): MockRepository<T> => ({
  find:    jest.fn(),
  findOne: jest.fn(),
  create:  jest.fn(),
  save:    jest.fn(),
  remove:  jest.fn(),
});

describe('UsersService', () => {
  let service: UsersService;
  let userRepository: MockRepository<User>;

  beforeEach(async () => {
    // ساخت TestingModule — قلب تست‌نویسی در NestJS
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        UsersService,
        {
          // به جای Repository واقعی، Mock ما را بده
          provide: getRepositoryToken(User),
          useValue: createMockRepository(),
        },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
    userRepository = module.get<MockRepository<User>>(getRepositoryToken(User));
  });

  // ── findAll ──────────────────────────────────────────────
  describe('findAll', () => {
    it('باید همه کاربران را برگرداند', async () => {
      // Arrange
      const mockUsers: User[] = [
        { id: 1, name: 'Ali',  email: 'ali@test.com',  age: 25, isActive: true },
        { id: 2, name: 'Sara', email: 'sara@test.com', age: 30, isActive: true },
      ];
      userRepository.find.mockResolvedValue(mockUsers);

      // Act
      const result = await service.findAll();

      // Assert
      expect(result).toEqual(mockUsers);
      expect(result).toHaveLength(2);
      expect(userRepository.find).toHaveBeenCalledTimes(1);
    });

    it('اگر کاربری نباشد آرایه خالی برگرداند', async () => {
      userRepository.find.mockResolvedValue([]);
      const result = await service.findAll();
      expect(result).toEqual([]);
    });
  });

  // ── findOne ──────────────────────────────────────────────
  describe('findOne', () => {
    it('اگر کاربر وجود داشت، او را برگرداند', async () => {
      const mockUser: User = { id: 1, name: 'Ali', email: 'ali@test.com', age: 25, isActive: true };
      userRepository.findOne.mockResolvedValue(mockUser);

      const result = await service.findOne(1);

      expect(result).toEqual(mockUser);
      expect(userRepository.findOne).toHaveBeenCalledWith({ where: { id: 1 } });
    });

    it('اگر کاربر پیدا نشد، NotFoundException throw کند', async () => {
      userRepository.findOne.mockResolvedValue(null); // دیتابیس null برمی‌گرداند

      await expect(service.findOne(999)).rejects.toThrow(NotFoundException);
      await expect(service.findOne(999)).rejects.toThrow('User with id 999 not found');
    });
  });

  // ── create ───────────────────────────────────────────────
  describe('create', () => {
    it('باید کاربر جدید ایجاد کند', async () => {
      const createData = { name: 'Ahmad', email: 'ahmad@test.com', age: 28 };
      const createdUser: User = { id: 3, ...createData, isActive: true };

      userRepository.create.mockReturnValue(createdUser); // sync
      userRepository.save.mockResolvedValue(createdUser);  // async

      const result = await service.create(createData);

      expect(result).toEqual(createdUser);
      expect(userRepository.create).toHaveBeenCalledWith(createData);
      expect(userRepository.save).toHaveBeenCalledWith(createdUser);
    });

    it('اگر name نداشت، BadRequestException throw کند', async () => {
      await expect(service.create({ email: 'test@test.com' }))
        .rejects.toThrow(BadRequestException);
    });

    it('اگر email نداشت، BadRequestException throw کند', async () => {
      await expect(service.create({ name: 'Ali' }))
        .rejects.toThrow(BadRequestException);
    });
  });
});
```

</div>

<div dir="rtl">

### jest.fn() — قدرت Mocking

`jest.fn()` ابزار اصلی برای ساخت تابع‌های جعلی است:

```typescript
describe('jest.fn() آموزش', () => {

  it('ساخت mock function ساده', () => {
    const mockFn = jest.fn();
    mockFn('hello');
    mockFn('world');

    expect(mockFn).toHaveBeenCalledTimes(2);
    expect(mockFn).toHaveBeenCalledWith('hello');
    expect(mockFn).toHaveBeenLastCalledWith('world');
    expect(mockFn).toHaveBeenNthCalledWith(1, 'hello');
  });

  it('تعریف مقدار بازگشتی', () => {
    const mockFn = jest.fn();

    // همیشه این مقدار را برمی‌گرداند
    mockFn.mockReturnValue('fixed value');
    expect(mockFn()).toBe('fixed value');

    // برای async
    mockFn.mockResolvedValue({ id: 1 });
    // معادل: mockFn.mockReturnValue(Promise.resolve({ id: 1 }));

    // رد کردن Promise
    mockFn.mockRejectedValue(new Error('DB Error'));
  });

  it('تعریف مقادیر مختلف برای هر بار صدا زدن', () => {
    const mockFn = jest.fn()
      .mockReturnValueOnce('first call')   // بار اول
      .mockReturnValueOnce('second call')  // بار دوم
      .mockReturnValue('default');          // بعد از آن

    expect(mockFn()).toBe('first call');
    expect(mockFn()).toBe('second call');
    expect(mockFn()).toBe('default');
    expect(mockFn()).toBe('default');
  });

  it('reset کردن mock', () => {
    const mockFn = jest.fn().mockReturnValue(42);
    mockFn();
    mockFn();

    // فقط تاریخچه را پاک می‌کند
    mockFn.mockClear();
    expect(mockFn).toHaveBeenCalledTimes(0); // ✓
    expect(mockFn()).toBe(42); // هنوز کار می‌کند

    // همه چیز را reset می‌کند
    mockFn.mockReset();
    expect(mockFn()).toBeUndefined(); // implementation هم reset شد
  });
});
```

### jest.spyOn — جاسوسی روی متدها

```typescript
describe('jest.spyOn', () => {
  class Calculator {
    add(a: number, b: number): number { return a + b; }
    subtract(a: number, b: number): number { return a - b; }
  }

  it('بررسی صدا زده شدن متد واقعی', () => {
    const calc = new Calculator();
    const spy = jest.spyOn(calc, 'add');

    const result = calc.add(2, 3);

    expect(result).toBe(5);                      // متد واقعی اجرا شد
    expect(spy).toHaveBeenCalledWith(2, 3);       // صدا زده شد
    expect(spy).toHaveBeenCalledTimes(1);

    spy.mockRestore(); // بعد از تست، restore کنید
  });

  it('override کردن پیاده‌سازی', () => {
    const calc = new Calculator();
    const spy = jest.spyOn(calc, 'add').mockReturnValue(100); // جعل!

    const result = calc.add(2, 3);
    expect(result).toBe(100); // جواب جعلی

    spy.mockRestore();
  });
});
```

### تست Controller

تست Controller کمی متفاوت است. معمولاً Service را Mock می‌کنیم و فقط منطق Controller را بررسی می‌کنیم:

**`src/users/users.controller.ts`**

```typescript
import { Controller, Get, Post, Delete, Param, Body, ParseIntPipe } from '@nestjs/common';
import { UsersService } from './users.service';

@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll() {
    return this.usersService.findAll();
  }

  @Get(':id')
  findOne(@Param('id', ParseIntPipe) id: number) {
    return this.usersService.findOne(id);
  }

  @Post()
  create(@Body() createUserDto: any) {
    return this.usersService.create(createUserDto);
  }
}
```

**`src/users/users.controller.spec.ts`**

```typescript
import { Test, TestingModule } from '@nestjs/testing';
import { UsersController } from './users.controller';
import { UsersService } from './users.service';

describe('UsersController', () => {
  let controller: UsersController;
  let usersService: jest.Mocked<UsersService>;

  beforeEach(async () => {
    // ساخت یک mock کامل از UsersService
    const mockUsersService = {
      findAll: jest.fn(),
      findOne: jest.fn(),
      create:  jest.fn(),
      remove:  jest.fn(),
    };

    const module: TestingModule = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [
        { provide: UsersService, useValue: mockUsersService },
      ],
    }).compile();

    controller  = module.get<UsersController>(UsersController);
    usersService = module.get(UsersService);
  });

  describe('findAll', () => {
    it('باید لیست کاربران را از service بگیرد', async () => {
      const mockUsers = [{ id: 1, name: 'Ali', email: 'ali@test.com' }];
      usersService.findAll.mockResolvedValue(mockUsers as any);

      const result = await controller.findAll();

      expect(result).toEqual(mockUsers);
      expect(usersService.findAll).toHaveBeenCalledTimes(1);
    });
  });

  describe('findOne', () => {
    it('باید یک کاربر را از service بگیرد', async () => {
      const mockUser = { id: 1, name: 'Ali', email: 'ali@test.com' };
      usersService.findOne.mockResolvedValue(mockUser as any);

      const result = await controller.findOne(1);

      expect(result).toEqual(mockUser);
      expect(usersService.findOne).toHaveBeenCalledWith(1);
    });
  });
});
```

---

## سطح ۳ — Integration / E2E Testing

در این سطح یاد می‌گیریم چطور کل برنامه را به صورت یکپارچه تست کنیم. یعنی یک درخواست HTTP واقعی می‌فرستیم و پاسخ کامل را بررسی می‌کنیم، مثل یک کاربر واقعی.

### تنظیمات E2E

**`test/jest-e2e.json`**

```json
{
  "moduleFileExtensions": ["js", "json", "ts"],
  "rootDir": ".",
  "testEnvironment": "node",
  "testRegex": ".e2e-spec.ts$",
  "transform": {
    "^.+\\.(t|j)s$": "ts-jest"
  },
  "testTimeout": 30000
}
```

</div>

<div dir="rtl">

### اولین E2E Test

**`test/users.e2e-spec.ts`**

```typescript
import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication, ValidationPipe } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from '../src/app.module';
import { getRepositoryToken } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from '../src/users/user.entity';

describe('UsersController (e2e)', () => {
  let app: INestApplication;
  let userRepository: Repository<User>;

  // قبل از همه تست‌ها: برنامه را راه‌اندازی کن
  beforeAll(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();

    // همان Pipe هایی که در main.ts دارید را اینجا هم اضافه کنید
    app.useGlobalPipes(new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true,
      transform: true,
    }));

    await app.init();

    userRepository = moduleFixture.get<Repository<User>>(getRepositoryToken(User));
  });

  // قبل از هر تست: دیتابیس را پاک کن
  beforeEach(async () => {
    await userRepository.query('DELETE FROM user');
  });

  // بعد از همه تست‌ها: برنامه را ببند
  afterAll(async () => {
    await app.close();
  });

  // ── GET /users ────────────────────────────────────────────
  describe('GET /users', () => {
    it('باید لیست خالی برگرداند وقتی کاربری نیست', async () => {
      const response = await request(app.getHttpServer())
        .get('/users')
        .expect(200);

      expect(response.body).toEqual([]);
    });

    it('باید لیست کاربران موجود را برگرداند', async () => {
      // Arrange: کاربر در دیتابیس می‌سازیم
      await userRepository.save([
        { name: 'Ali',  email: 'ali@test.com',  age: 25 },
        { name: 'Sara', email: 'sara@test.com', age: 30 },
      ]);

      // Act & Assert
      const response = await request(app.getHttpServer())
        .get('/users')
        .expect(200);

      expect(response.body).toHaveLength(2);
      expect(response.body[0]).toMatchObject({ name: 'Ali', email: 'ali@test.com' });
    });
  });

  // ── POST /users ───────────────────────────────────────────
  describe('POST /users', () => {
    it('باید کاربر جدید بسازد و 201 برگرداند', async () => {
      const createDto = { name: 'Ahmad', email: 'ahmad@test.com', age: 28 };

      const response = await request(app.getHttpServer())
        .post('/users')
        .send(createDto)
        .expect(201);

      expect(response.body).toMatchObject(createDto);
      expect(response.body.id).toBeDefined();

      // بررسی اینکه واقعاً در دیتابیس ذخیره شده
      const savedUser = await userRepository.findOne({ where: { email: 'ahmad@test.com' } });
      expect(savedUser).toBeDefined();
      expect(savedUser.name).toBe('Ahmad');
    });

    it('باید 400 برگرداند وقتی email وجود ندارد', async () => {
      const response = await request(app.getHttpServer())
        .post('/users')
        .send({ name: 'Ali' })  // email نداریم
        .expect(400);

      expect(response.body.message).toBeDefined();
    });
  });

  // ── GET /users/:id ────────────────────────────────────────
  describe('GET /users/:id', () => {
    it('باید یک کاربر را با id پیدا کند', async () => {
      const user = await userRepository.save({ name: 'Ali', email: 'ali@test.com', age: 25 });

      const response = await request(app.getHttpServer())
        .get(`/users/${user.id}`)
        .expect(200);

      expect(response.body).toMatchObject({ name: 'Ali', email: 'ali@test.com' });
    });

    it('باید 404 برگرداند وقتی کاربر وجود ندارد', async () => {
      await request(app.getHttpServer())
        .get('/users/99999')
        .expect(404);
    });

    it('باید 400 برگرداند وقتی id معتبر نیست', async () => {
      await request(app.getHttpServer())
        .get('/users/invalid-id')
        .expect(400);
    });
  });

  // ── DELETE /users/:id ─────────────────────────────────────
  describe('DELETE /users/:id', () => {
    it('باید کاربر را حذف کند', async () => {
      const user = await userRepository.save({ name: 'Ali', email: 'ali@test.com', age: 25 });

      await request(app.getHttpServer())
        .delete(`/users/${user.id}`)
        .expect(200);

      const deletedUser = await userRepository.findOne({ where: { id: user.id } });
      expect(deletedUser).toBeNull();
    });
  });
});
```

### Authentication در E2E Tests

وقتی endpoint ها نیاز به Authentication دارند، باید ابتدا Login کنید و Token را نگه دارید:

```typescript
describe('Protected Endpoints (e2e)', () => {
  let app: INestApplication;
  let accessToken: string;
  let adminToken: string;

  beforeAll(async () => {
    // ... راه‌اندازی app

    // Login و گرفتن token
    const loginResponse = await request(app.getHttpServer())
      .post('/auth/login')
      .send({ email: 'user@test.com', password: 'password123' })
      .expect(200);
    accessToken = loginResponse.body.access_token;

    const adminLoginResponse = await request(app.getHttpServer())
      .post('/auth/login')
      .send({ email: 'admin@test.com', password: 'admin123' })
      .expect(200);
    adminToken = adminLoginResponse.body.access_token;
  });

  it('بدون token باید 401 برگرداند', async () => {
    await request(app.getHttpServer())
      .get('/profile')
      .expect(401);
  });

  it('با token معتبر باید 200 برگرداند', async () => {
    await request(app.getHttpServer())
      .get('/profile')
      .set('Authorization', `Bearer ${accessToken}`)  // token را اضافه کنید
      .expect(200);
  });

  it('کاربر عادی نباید به endpoint ادمین دسترسی داشته باشد', async () => {
    await request(app.getHttpServer())
      .get('/admin/users')
      .set('Authorization', `Bearer ${accessToken}`)
      .expect(403);
  });

  it('ادمین باید به endpoint ادمین دسترسی داشته باشد', async () => {
    await request(app.getHttpServer())
      .get('/admin/users')
      .set('Authorization', `Bearer ${adminToken}`)
      .expect(200);
  });
});
```

---

## سطح ۴ — تکنیک‌های پیشرفته

### TDD — Test Driven Development

TDD یعنی اول تست بنویس، بعد کد. این فلسفه سه مرحله دارد که به آن Red-Green-Refactor می‌گویند:

```typescript
// مرحله ۱ — RED: تست بنویس که FAIL می‌شود
// (کد هنوز وجود ندارد)
it('باید قیمت با تخفیف را محاسبه کند', () => {
  const priceCalculator = new PriceCalculator();
  // این تست fail می‌شود چون PriceCalculator وجود ندارد
  expect(priceCalculator.applyDiscount(100, 20)).toBe(80);
});

// مرحله ۲ — GREEN: کمترین کدی بنویس که تست را pass کند
class PriceCalculator {
  applyDiscount(price: number, discountPercent: number): number {
    return price - (price * discountPercent / 100);
  }
}

// مرحله ۳ — REFACTOR: کد را بهبود بده بدون اینکه تست fail شود
class PriceCalculator {
  applyDiscount(price: number, discountPercent: number): number {
    this.validateInputs(price, discountPercent);
    const discount = price * (discountPercent / 100);
    return parseFloat((price - discount).toFixed(2));
  }

  private validateInputs(price: number, discountPercent: number): void {
    if (price < 0) throw new Error('Price cannot be negative');
    if (discountPercent < 0 || discountPercent > 100) {
      throw new Error('Discount must be between 0 and 100');
    }
  }
}
```

</div>

<div dir="rtl">

### تست Guards

Guard ها مسئول کنترل دسترسی هستند. در Unit Test آن‌ها، Context را Mock می‌کنیم:

**`src/auth/jwt-auth.guard.spec.ts`**

```typescript
import { JwtAuthGuard } from './jwt-auth.guard';
import { ExecutionContext } from '@nestjs/common';
import { JwtService } from '@nestjs/jwt';

// ساخت یک mock از ExecutionContext
const createMockExecutionContext = (authHeader?: string): ExecutionContext => ({
  switchToHttp: () => ({
    getRequest: () => ({
      headers: { authorization: authHeader },
    }),
  }),
  getHandler: () => ({}),
  getClass: () => ({}),
} as any);

describe('JwtAuthGuard', () => {
  let guard: JwtAuthGuard;
  let jwtService: jest.Mocked<JwtService>;

  beforeEach(() => {
    jwtService = { verify: jest.fn() } as any;
    guard = new JwtAuthGuard(jwtService);
  });

  it('باید دسترسی را با token معتبر بدهد', async () => {
    jwtService.verify.mockReturnValue({ userId: 1, email: 'test@test.com' });
    const context = createMockExecutionContext('Bearer valid.token.here');

    const result = await guard.canActivate(context);
    expect(result).toBe(true);
  });

  it('باید دسترسی را بدون token رد کند', async () => {
    const context = createMockExecutionContext(); // بدون header

    await expect(guard.canActivate(context)).rejects.toThrow();
  });

  it('باید دسترسی را با token نامعتبر رد کند', async () => {
    jwtService.verify.mockImplementation(() => {
      throw new Error('invalid token');
    });
    const context = createMockExecutionContext('Bearer invalid.token');

    await expect(guard.canActivate(context)).rejects.toThrow();
  });
});
```

### تست Pipes

Pipe ها مسئول validation و transformation هستند:

```typescript
import { ParsePositiveIntPipe } from './parse-positive-int.pipe';
import { BadRequestException } from '@nestjs/common';

// فرض: یک Pipe ساخته‌ایم که فقط عدد مثبت قبول می‌کند
describe('ParsePositiveIntPipe', () => {
  let pipe: ParsePositiveIntPipe;

  beforeEach(() => {
    pipe = new ParsePositiveIntPipe();
  });

  it('باید عدد مثبت را بپذیرد', () => {
    expect(pipe.transform('5', {} as any)).toBe(5);
    expect(pipe.transform('100', {} as any)).toBe(100);
  });

  it('باید عدد منفی را رد کند', () => {
    expect(() => pipe.transform('-1', {} as any)).toThrow(BadRequestException);
  });

  it('باید صفر را رد کند', () => {
    expect(() => pipe.transform('0', {} as any)).toThrow(BadRequestException);
  });

  it('باید string غیر عددی را رد کند', () => {
    expect(() => pipe.transform('abc', {} as any)).toThrow(BadRequestException);
  });
});
```

### تست Interceptors

```typescript
import { LoggingInterceptor } from './logging.interceptor';
import { ExecutionContext, CallHandler } from '@nestjs/common';
import { of } from 'rxjs';

describe('LoggingInterceptor', () => {
  let interceptor: LoggingInterceptor;

  beforeEach(() => {
    interceptor = new LoggingInterceptor();
    jest.spyOn(console, 'log').mockImplementation(() => {}); // console را mock کن
  });

  afterEach(() => {
    jest.restoreAllMocks();
  });

  it('باید response را بدون تغییر برگرداند', async () => {
    const mockContext = {
      switchToHttp: () => ({
        getRequest: () => ({ method: 'GET', url: '/users' }),
      }),
    } as ExecutionContext;

    const mockCallHandler: CallHandler = {
      handle: () => of({ id: 1, name: 'Ali' }), // Observable
    };

    const result$ = interceptor.intercept(mockContext, mockCallHandler);
    const result = await result$.toPromise();

    expect(result).toEqual({ id: 1, name: 'Ali' });
    expect(console.log).toHaveBeenCalled(); // بررسی اینکه log شده
  });
});
```

### Faker.js — دیتای تستی واقع‌گرایانه

به جای نوشتن دیتای ثابت، از Faker.js برای تولید دیتای تصادفی و واقع‌گرایانه استفاده کنید:

```typescript
import { faker } from '@faker-js/faker';

// Factory function برای ساخت User تستی
function createUserFactory(overrides: Partial<User> = {}): User {
  return {
    id:       faker.number.int({ min: 1, max: 10000 }),
    name:     faker.person.fullName(),
    email:    faker.internet.email(),
    age:      faker.number.int({ min: 18, max: 80 }),
    isActive: faker.datatype.boolean(),
    ...overrides,  // می‌توان بعضی field ها را override کرد
  };
}

describe('UsersService با Faker', () => {
  it('باید یک کاربر واقعی بسازد', async () => {
    const mockUser = createUserFactory({ isActive: true });
    userRepository.save.mockResolvedValue(mockUser);

    const result = await service.create({
      name:  mockUser.name,
      email: mockUser.email,
    });

    expect(result.name).toBe(mockUser.name);
    expect(result.email).toBe(mockUser.email);
  });

  it('باید ۱۰ کاربر تصادفی پردازش کند', async () => {
    const mockUsers = Array.from({ length: 10 }, () => createUserFactory());
    userRepository.find.mockResolvedValue(mockUsers);

    const result = await service.findAll();
    expect(result).toHaveLength(10);
  });
});
```

### Test Coverage — تحلیل پوشش کد

Coverage نشان می‌دهد چند درصد از کد شما توسط تست‌ها اجرا شده است:

```bash
# اجرا با coverage
npm run test:cov

# نتیجه مثال:
# --------------------|---------|----------|---------|---------| 
# File                | % Stmts | % Branch | % Funcs | % Lines |
# --------------------|---------|----------|---------|---------| 
# users/              |         |          |         |         |
#  users.service.ts   |   95.2  |   88.5   |   100   |   94.7  |
#  users.controller.ts|   100   |   100    |   100   |   100   |
# --------------------|---------|----------|---------|---------| 
```

تنظیمات Coverage در `package.json`:

```json
"jest": {
  "coverageThreshold": {
    "global": {
      "statements": 80,
      "branches": 75,
      "functions": 80,
      "lines": 80
    }
  },
  "collectCoverageFrom": [
    "src/**/*.ts",
    "!src/**/*.module.ts",
    "!src/main.ts",
    "!src/**/*.dto.ts",
    "!src/**/*.entity.ts"
  ]
}
```

> 💡 **هدف‌گذاری Coverage** — برای پروژه‌های production، هدف‌گذاری ۸۰٪+ معقول است. ۱۰۰٪ همیشه ممکن یا مفید نیست. مهم‌تر از عدد Coverage، کیفیت تست‌ها است.

---

## TestContainers — دیتابیس واقعی در تست

TestContainers یک کتابخانه است که به شما امکان می‌دهد دیتابیس واقعی (مثل PostgreSQL) را داخل Docker در زمان اجرای تست بالا بیاورید. این بهترین روش برای E2E Test هایی است که به دیتابیس واقعی نیاز دارند.

```bash
# نصب
npm install --save-dev testcontainers
```

```typescript
import { PostgreSqlContainer, StartedPostgreSqlContainer } from 'testcontainers';
import { Test, TestingModule } from '@nestjs/testing';
import { TypeOrmModule } from '@nestjs/typeorm';

describe('UsersService (با دیتابیس واقعی)', () => {
  let container: StartedPostgreSqlContainer;
  let app: INestApplication;

  // یک بار قبل از همه تست‌ها، Docker container را بالا می‌آوریم
  beforeAll(async () => {
    container = await new PostgreSqlContainer()
      .withDatabase('test_db')
      .withUsername('test_user')
      .withPassword('test_pass')
      .start();

    const moduleFixture = await Test.createTestingModule({
      imports: [
        TypeOrmModule.forRoot({
          type: 'postgres',
          host:     container.getHost(),
          port:     container.getPort(),
          username: container.getUsername(),
          password: container.getPassword(),
          database: container.getDatabase(),
          entities:     [User],
          synchronize:  true,  // فقط برای تست!
        }),
        UsersModule,
      ],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  }, 60000); // ۶۰ ثانیه timeout برای بالا آمدن Docker

  afterAll(async () => {
    await app.close();
    await container.stop(); // Docker container را خاموش کن
  });

  it('باید با دیتابیس واقعی کار کند', async () => {
    const response = await request(app.getHttpServer())
      .post('/users')
      .send({ name: 'Ali', email: 'ali@test.com', age: 25 })
      .expect(201);

    expect(response.body.id).toBeDefined();
  });
});
```

---

## بهترین شیوه‌ها و نکات کلیدی

### اصول نوشتن تست خوب

| اصل | توضیح |
|-----|-------|
| یک Assertion در هر تست | هر تست باید فقط یک چیز را بررسی کند. اگر چند expect دارید، احتمالاً باید تست را تقسیم کنید. |
| نام معنادار | نام تست باید توضیح دهد: چه چیزی، در چه شرایطی، چه انتظاری. مثال: `findOne - when user not exists - should throw NotFoundException` |
| ایزوله بودن | هر تست باید مستقل باشد. اگر ترتیب تست‌ها اهمیت دارد، مشکل دارید. |
| F.I.R.S.T | Fast, Independent, Repeatable, Self-validating, Timely. تست‌های خوب این ۵ خاصیت را دارند. |
| بررسی Edge Cases | همیشه حالت‌های مرزی را تست کنید: null, undefined, آرایه خالی، عدد منفی. |
| آرایش قبل از تست | در `beforeEach` دیتابیس را reset کنید تا تست‌ها به هم وابسته نباشند. |

### Anti-patterns — اشتباهات رایج

```typescript
// ❌ اشتباه: تست بدون Assertion
it('کاربر ساخته می‌شود', async () => {
  await service.create({ name: 'Ali', email: 'ali@test.com' });
  // هیچ expect ای نداریم! این تست همیشه pass می‌شود
});

// ✅ درست:
it('باید کاربر ایجاد کند و id برگرداند', async () => {
  const result = await service.create({ name: 'Ali', email: 'ali@test.com' });
  expect(result.id).toBeDefined();
  expect(result.name).toBe('Ali');
});

// ─────────────────────────────────────────────

// ❌ اشتباه: تست وابسته به تست دیگر
let createdUserId: number;
it('کاربر می‌سازد', async () => {
  const user = await service.create({ name: 'Ali' });
  createdUserId = user.id; // این global state خطرناک است!
});
it('کاربر را پیدا می‌کند', async () => {
  // اگر تست قبلی fail شود، این هم fail می‌شود
  const user = await service.findOne(createdUserId);
});

// ✅ درست: هر تست باید دیتای خودش را بسازد
it('کاربر ساخته شده را باید پیدا کند', async () => {
  const created = await service.create({ name: 'Ali', email: 'ali@test.com' });
  const found   = await service.findOne(created.id);
  expect(found.name).toBe('Ali');
});
```

---

## جدول مقایسه انواع تست

| ویژگی | Unit Test | Integration | E2E Test |
|-------|-----------|-------------|----------|
| سرعت | ⚡ خیلی سریع | 🔄 متوسط | 🐢 کند |
| وابستگی | ایزوله (Mock) | بعضی وابستگی‌ها | کل سیستم |
| پیچیدگی | کم | متوسط | زیاد |
| پوشش | یک واحد | چند واحد | کل flow |
| ابزار | Jest + Mock | Jest + Module | Supertest + DB |
| تعداد پیشنهادی | زیاد (۷۰٪) | متوسط (۲۰٪) | کم (۱۰٪) |

---

## Cheat Sheet — مرجع سریع

### مهم‌ترین Matchers

```typescript
// مقادیر
expect(val).toBe(x)              // ===
expect(val).toEqual(x)           // deep equality
expect(val).toBeNull()
expect(val).toBeUndefined()
expect(val).toBeDefined()
expect(val).toBeTruthy()
expect(val).toBeFalsy()

// اعداد
expect(n).toBeGreaterThan(x)
expect(n).toBeLessThan(x)
expect(n).toBeCloseTo(x, digits)

// رشته‌ها
expect(str).toMatch(/regex/)
expect(str).toHaveLength(n)
expect(str).toContain('sub')

// آرایه‌ها
expect(arr).toContain(item)
expect(arr).toContainEqual({ id: 1 })
expect(arr).toHaveLength(n)

// Object
expect(obj).toMatchObject({ key: val })  // partial match
expect(obj).toHaveProperty('key', val)

// Exception
expect(() => fn()).toThrow()
expect(() => fn()).toThrow(Error)
expect(() => fn()).toThrow('message')
await expect(asyncFn()).rejects.toThrow()

// Mock
expect(mockFn).toHaveBeenCalled()
expect(mockFn).toHaveBeenCalledTimes(n)
expect(mockFn).toHaveBeenCalledWith(arg1, arg2)
expect(mockFn).toHaveBeenLastCalledWith(arg)

// نقیض
expect(val).not.toBe(x)
expect(mockFn).not.toHaveBeenCalled()
```

### مهم‌ترین دستورات Mock

```typescript
// ساخت
const fn = jest.fn();
const fn = jest.fn().mockReturnValue(42);
const fn = jest.fn().mockResolvedValue({ id: 1 });
const fn = jest.fn().mockRejectedValue(new Error('err'));
const fn = jest.fn().mockImplementation((x) => x * 2);

// بار اول، بار دوم، ...
fn.mockReturnValueOnce(1).mockReturnValueOnce(2).mockReturnValue(0);

// Spy
const spy = jest.spyOn(object, 'method');
const spy = jest.spyOn(object, 'method').mockReturnValue(42);
spy.mockRestore();

// Reset
fn.mockClear();   // فقط call history را پاک می‌کند
fn.mockReset();   // history + implementation
fn.mockRestore(); // فقط برای spyOn - به حالت اصلی برمی‌گرداند

// Mock کردن module
jest.mock('./users.service');
jest.mock('@nestjs/typeorm', () => ({ InjectRepository: () => () => {} }));
```

---

## سطح ۵ — تکنیک‌های تکمیلی

### تست با دیتابیس In-Memory (SQLite)

به جای Mock کردن Repository یا راه‌اندازی Docker، می‌توانید از SQLite In-Memory استفاده کنید. این روش سریع‌تر از TestContainers و واقعی‌تر از Mock است — بهترین گزینه برای Integration Test های سبک.

```bash
npm install --save-dev better-sqlite3
npm install --save-dev @types/better-sqlite3
```

```typescript
// test/helpers/create-test-app.ts
import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication, ValidationPipe } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from '../../src/users/user.entity';

export async function createTestApp(modules: any[]): Promise<INestApplication> {
  const moduleFixture: TestingModule = await Test.createTestingModule({
    imports: [
      // دیتابیس SQLite In-Memory — هر بار تست تازه شروع می‌شود
      TypeOrmModule.forRoot({
        type: 'better-sqlite3',
        database: ':memory:',   // در RAM نگه می‌دارد، روی دیسک نمی‌نویسد
        entities: [User],
        synchronize: true,      // schema را خودکار می‌سازد
        dropSchema: true,       // قبل از هر اجرا schema را پاک می‌کند
      }),
      ...modules,
    ],
  }).compile();

  const app = moduleFixture.createNestApplication();
  app.useGlobalPipes(new ValidationPipe({ whitelist: true, transform: true }));
  await app.init();
  return app;
}
```

```typescript
// src/users/users.integration.spec.ts
import * as request from 'supertest';
import { INestApplication } from '@nestjs/common';
import { createTestApp } from '../../test/helpers/create-test-app';
import { UsersModule } from './users.module';

describe('Users Integration (SQLite)', () => {
  let app: INestApplication;

  beforeAll(async () => {
    app = await createTestApp([UsersModule]);
  });

  afterAll(async () => {
    await app.close();
  });

  it('باید کاربر بسازد و بازیابی کند', async () => {
    // ساخت کاربر
    const createRes = await request(app.getHttpServer())
      .post('/users')
      .send({ name: 'Ali', email: 'ali@test.com', age: 25 })
      .expect(201);

    const userId = createRes.body.id;

    // بازیابی همان کاربر
    const getRes = await request(app.getHttpServer())
      .get(`/users/${userId}`)
      .expect(200);

    expect(getRes.body).toMatchObject({ name: 'Ali', email: 'ali@test.com' });
  });
});
```

> 💡 **چه وقت SQLite بهتر از Mock است؟** وقتی می‌خواهید query های واقعی TypeORM (مثل relation ها، pagination، filter) را تست کنید. Mock فقط رفتار ساده را شبیه‌سازی می‌کند.

---

### تست Exception Filters

Exception Filter ها مسئول تبدیل خطاها به response های HTTP هستند. باید مطمئن شویم فرمت خروجی درست است.

```typescript
// src/common/filters/http-exception.filter.ts
import { ExceptionFilter, Catch, ArgumentsHost, HttpException } from '@nestjs/common';
import { Request, Response } from 'express';

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx      = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request  = ctx.getRequest<Request>();
    const status   = exception.getStatus();

    response.status(status).json({
      statusCode: status,
      timestamp:  new Date().toISOString(),
      path:       request.url,
      message:    exception.message,
    });
  }
}
```

```typescript
// src/common/filters/http-exception.filter.spec.ts
import { HttpExceptionFilter } from './http-exception.filter';
import { HttpException, HttpStatus, ArgumentsHost } from '@nestjs/common';

// ساخت mock از ArgumentsHost
const createMockArgumentsHost = (url = '/test'): ArgumentsHost => {
  const mockJson = jest.fn();
  const mockStatus = jest.fn().mockReturnValue({ json: mockJson });

  return {
    switchToHttp: () => ({
      getResponse: () => ({ status: mockStatus }),
      getRequest:  () => ({ url }),
    }),
  } as any;
};

describe('HttpExceptionFilter', () => {
  let filter: HttpExceptionFilter;

  beforeEach(() => {
    filter = new HttpExceptionFilter();
    jest.useFakeTimers(); // زمان را ثابت می‌کنیم
    jest.setSystemTime(new Date('2024-01-01T00:00:00.000Z'));
  });

  afterEach(() => {
    jest.useRealTimers();
  });

  it('باید response با فرمت صحیح برگرداند', () => {
    const exception = new HttpException('Not Found', HttpStatus.NOT_FOUND);
    const host = createMockArgumentsHost('/users/99');

    filter.catch(exception, host);

    const mockStatus = host.switchToHttp().getResponse().status as jest.Mock;
    const mockJson   = mockStatus.mock.results[0].value.json as jest.Mock;

    expect(mockStatus).toHaveBeenCalledWith(404);
    expect(mockJson).toHaveBeenCalledWith({
      statusCode: 404,
      timestamp:  '2024-01-01T00:00:00.000Z',
      path:       '/users/99',
      message:    'Not Found',
    });
  });

  it('باید status code درست را برگرداند', () => {
    const exception = new HttpException('Forbidden', HttpStatus.FORBIDDEN);
    const host = createMockArgumentsHost();

    filter.catch(exception, host);

    const mockStatus = host.switchToHttp().getResponse().status as jest.Mock;
    expect(mockStatus).toHaveBeenCalledWith(403);
  });
});
```

**تست E2E با Filter:**

```typescript
// بررسی اینکه Filter روی app نصب شده درست کار می‌کند
it('باید خطای 404 را با فرمت سفارشی برگرداند', async () => {
  const response = await request(app.getHttpServer())
    .get('/users/99999')
    .expect(404);

  expect(response.body).toMatchObject({
    statusCode: 404,
    path:       '/users/99999',
    message:    expect.any(String),
    timestamp:  expect.any(String),
  });
});
```

---

### Mock کامل ماژول با jest.mock()

`jest.mock()` کل یک ماژول را جایگزین می‌کند. برای third-party library ها یا ماژول‌های داخلی که نمی‌خواهید واقعاً اجرا شوند ایده‌آل است.

```typescript
// ── مثال ۱: Mock کردن یک ماژول داخلی ──────────────────────

// src/notifications/notifications.service.ts
import { EmailService } from '../email/email.service';

// در فایل تست:
jest.mock('../email/email.service'); // کل ماژول را mock می‌کند

describe('NotificationsService', () => {
  it('باید email بفرستد', async () => {
    const emailService = new EmailService() as jest.Mocked<EmailService>;
    // EmailService.prototype.send به صورت خودکار mock شده
    emailService.send.mockResolvedValue(undefined);

    // ...
  });
});
```

```typescript
// ── مثال ۲: Mock با factory function ──────────────────────

jest.mock('@nestjs/jwt', () => ({
  JwtService: jest.fn().mockImplementation(() => ({
    sign:   jest.fn().mockReturnValue('mocked.jwt.token'),
    verify: jest.fn().mockReturnValue({ userId: 1, email: 'test@test.com' }),
  })),
}));

describe('AuthService', () => {
  it('باید token بسازد', async () => {
    const { JwtService } = require('@nestjs/jwt');
    const jwtService = new JwtService();

    const token = jwtService.sign({ userId: 1 });
    expect(token).toBe('mocked.jwt.token');
  });
});
```

```typescript
// ── مثال ۳: Mock جزئی — فقط بعضی export ها ──────────────

jest.mock('../utils/date.utils', () => ({
  ...jest.requireActual('../utils/date.utils'), // بقیه را واقعی نگه دار
  getCurrentDate: jest.fn().mockReturnValue(new Date('2024-01-01')), // فقط این را mock کن
}));

describe('ReportService', () => {
  it('باید گزارش با تاریخ ثابت بسازد', async () => {
    // getCurrentDate همیشه 2024-01-01 برمی‌گرداند
    const report = await service.generateDailyReport();
    expect(report.date).toBe('2024-01-01');
  });
});
```

```typescript
// ── مثال ۴: Mock کردن TypeORM decorators ──────────────────

// وقتی entity ها decorator دارند و در تست مشکل ایجاد می‌کنند
jest.mock('@nestjs/typeorm', () => ({
  InjectRepository: () => () => {},  // decorator را به تابع خالی تبدیل می‌کند
  getRepositoryToken: jest.requireActual('@nestjs/typeorm').getRepositoryToken,
}));
```

> 💡 **نکته مهم** — `jest.mock()` باید در بالای فایل و خارج از هر `describe` یا `it` باشد. Jest آن را به بالای فایل hoist می‌کند.

---

### تست با ConfigService و متغیرهای محیطی

تقریباً هر پروژه NestJS از `ConfigService` استفاده می‌کند. باید بدانیم چطور آن را در تست‌ها مدیریت کنیم.

```typescript
// ── روش ۱: Mock کردن ConfigService ────────────────────────

import { ConfigService } from '@nestjs/config';

describe('DatabaseService', () => {
  let service: DatabaseService;
  let configService: jest.Mocked<ConfigService>;

  beforeEach(async () => {
    const mockConfigService = {
      get: jest.fn((key: string) => {
        const config = {
          'DB_HOST':     'localhost',
          'DB_PORT':     5432,
          'DB_NAME':     'test_db',
          'JWT_SECRET':  'test-secret-key',
          'APP_ENV':     'test',
        };
        return config[key];
      }),
      getOrThrow: jest.fn((key: string) => {
        const value = mockConfigService.get(key);
        if (!value) throw new Error(`Config key "${key}" not found`);
        return value;
      }),
    };

    const module = await Test.createTestingModule({
      providers: [
        DatabaseService,
        { provide: ConfigService, useValue: mockConfigService },
      ],
    }).compile();

    service       = module.get<DatabaseService>(DatabaseService);
    configService = module.get(ConfigService);
  });

  it('باید connection string درست بسازد', () => {
    const connString = service.getConnectionString();
    expect(connString).toBe('postgresql://localhost:5432/test_db');
    expect(configService.get).toHaveBeenCalledWith('DB_HOST');
  });
});
```

```typescript
// ── روش ۲: استفاده از ConfigModule واقعی با .env.test ──────

// .env.test
// DB_HOST=localhost
// DB_PORT=5432
// JWT_SECRET=test-only-secret

import { ConfigModule } from '@nestjs/config';

describe('AuthService (با ConfigModule واقعی)', () => {
  beforeEach(async () => {
    const module = await Test.createTestingModule({
      imports: [
        ConfigModule.forRoot({
          envFilePath: '.env.test',  // فایل env مخصوص تست
          isGlobal: true,
        }),
      ],
      providers: [AuthService],
    }).compile();
    // ...
  });
});
```

```typescript
// ── روش ۳: Override کردن متغیرهای محیطی در تست ────────────

describe('FeatureFlagService', () => {
  const originalEnv = process.env;

  beforeEach(() => {
    // کپی از env اصلی
    process.env = { ...originalEnv };
  });

  afterEach(() => {
    // بازگرداندن env اصلی
    process.env = originalEnv;
  });

  it('باید feature را فعال کند وقتی flag روشن است', () => {
    process.env.FEATURE_NEW_UI = 'true';
    expect(service.isEnabled('NEW_UI')).toBe(true);
  });

  it('باید feature را غیرفعال کند وقتی flag خاموش است', () => {
    process.env.FEATURE_NEW_UI = 'false';
    expect(service.isEnabled('NEW_UI')).toBe(false);
  });
});
```

---

### تست Middleware

Middleware قبل از رسیدن request به Controller اجرا می‌شود. تست آن شبیه تست Guard است:

```typescript
// src/common/middleware/logger.middleware.ts
import { Injectable, NestMiddleware } from '@nestjs/common';
import { Request, Response, NextFunction } from 'express';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    const start = Date.now();
    console.log(`→ ${req.method} ${req.url}`);

    res.on('finish', () => {
      const duration = Date.now() - start;
      console.log(`← ${res.statusCode} ${req.url} (${duration}ms)`);
    });

    next();
  }
}
```

```typescript
// src/common/middleware/logger.middleware.spec.ts
import { LoggerMiddleware } from './logger.middleware';

describe('LoggerMiddleware', () => {
  let middleware: LoggerMiddleware;
  let mockRequest: Partial<Request>;
  let mockResponse: Partial<Response>;
  let nextFunction: jest.Mock;

  beforeEach(() => {
    middleware = new LoggerMiddleware();

    mockRequest = {
      method: 'GET',
      url:    '/users',
    };

    // شبیه‌سازی EventEmitter برای res.on('finish')
    const listeners: Record<string, Function[]> = {};
    mockResponse = {
      statusCode: 200,
      on: jest.fn((event: string, cb: Function) => {
        listeners[event] = listeners[event] || [];
        listeners[event].push(cb);
      }),
      emit: jest.fn((event: string) => {
        (listeners[event] || []).forEach(cb => cb());
      }),
    } as any;

    nextFunction = jest.fn();
    jest.spyOn(console, 'log').mockImplementation(() => {});
  });

  afterEach(() => jest.restoreAllMocks());

  it('باید next() را صدا بزند', () => {
    middleware.use(mockRequest as any, mockResponse as any, nextFunction);
    expect(nextFunction).toHaveBeenCalledTimes(1);
  });

  it('باید request را log کند', () => {
    middleware.use(mockRequest as any, mockResponse as any, nextFunction);
    expect(console.log).toHaveBeenCalledWith('→ GET /users');
  });

  it('باید response را بعد از finish log کند', () => {
    middleware.use(mockRequest as any, mockResponse as any, nextFunction);
    (mockResponse as any).emit('finish'); // رویداد finish را شبیه‌سازی می‌کنیم
    expect(console.log).toHaveBeenCalledWith(expect.stringMatching(/← 200 \/users/));
  });
});
```

**تست E2E که Middleware را بررسی می‌کند:**

```typescript
it('باید header های درست را اضافه کند', async () => {
  const response = await request(app.getHttpServer())
    .get('/users')
    .expect(200);

  // بررسی header هایی که middleware اضافه کرده
  expect(response.headers['x-request-id']).toBeDefined();
  expect(response.headers['x-response-time']).toBeDefined();
});
```

---

### تست Event و Queue با BullMQ

BullMQ یکی از پرکاربردترین ابزارها برای پردازش صف در NestJS است. تست آن نیاز به Mock کردن Queue و Worker دارد.

```bash
npm install --save-dev @golevelup/ts-jest
```

```typescript
// src/email/email.processor.ts
import { Processor, WorkerHost } from '@nestjs/bullmq';
import { Job } from 'bullmq';

@Processor('email')
export class EmailProcessor extends WorkerHost {
  async process(job: Job): Promise<void> {
    const { to, subject, body } = job.data;
    // ارسال ایمیل واقعی
    await this.sendEmail(to, subject, body);
  }

  private async sendEmail(to: string, subject: string, body: string) {
    // پیاده‌سازی ارسال ایمیل
  }
}
```

```typescript
// src/email/email.processor.spec.ts
import { EmailProcessor } from './email.processor';
import { Job } from 'bullmq';

describe('EmailProcessor', () => {
  let processor: EmailProcessor;

  beforeEach(() => {
    processor = new EmailProcessor();
    // mock کردن متد private
    jest.spyOn(processor as any, 'sendEmail').mockResolvedValue(undefined);
  });

  it('باید job را پردازش کند', async () => {
    const mockJob = {
      data: {
        to:      'user@test.com',
        subject: 'خوش آمدید',
        body:    'به سایت ما خوش آمدید',
      },
    } as Job;

    await processor.process(mockJob);

    expect((processor as any).sendEmail).toHaveBeenCalledWith(
      'user@test.com',
      'خوش آمدید',
      'به سایت ما خوش آمدید',
    );
  });

  it('باید خطا را propagate کند', async () => {
    jest.spyOn(processor as any, 'sendEmail')
      .mockRejectedValue(new Error('SMTP Error'));

    const mockJob = {
      data: { to: 'user@test.com', subject: 'test', body: 'test' },
    } as Job;

    await expect(processor.process(mockJob)).rejects.toThrow('SMTP Error');
  });
});
```

```typescript
// src/users/users.service.spec.ts — تست اضافه کردن job به Queue
import { getQueueToken } from '@nestjs/bullmq';

describe('UsersService با Queue', () => {
  let service: UsersService;
  let emailQueue: { add: jest.Mock };

  beforeEach(async () => {
    emailQueue = { add: jest.fn().mockResolvedValue({ id: 'job-1' }) };

    const module = await Test.createTestingModule({
      providers: [
        UsersService,
        { provide: getRepositoryToken(User), useValue: createMockRepository() },
        { provide: getQueueToken('email'),   useValue: emailQueue },
      ],
    }).compile();

    service = module.get<UsersService>(UsersService);
  });

  it('باید بعد از ثبت‌نام، job ایمیل خوش‌آمدگویی اضافه کند', async () => {
    const userData = { name: 'Ali', email: 'ali@test.com', age: 25 };
    userRepository.create.mockReturnValue({ id: 1, ...userData, isActive: true });
    userRepository.save.mockResolvedValue({ id: 1, ...userData, isActive: true });

    await service.register(userData);

    expect(emailQueue.add).toHaveBeenCalledWith('welcome', {
      to:      'ali@test.com',
      subject: expect.any(String),
    });
  });
});
```

---

### Database Seeding و Factory Pattern پیشرفته

برای E2E Test های پیچیده، به یک سیستم Seeding قوی نیاز دارید که دیتای واقع‌گرایانه بسازد:

```typescript
// test/factories/user.factory.ts
import { faker } from '@faker-js/faker';
import { DataSource } from 'typeorm';
import { User } from '../../src/users/user.entity';

export class UserFactory {
  constructor(private readonly dataSource: DataSource) {}

  // ساخت یک user بدون ذخیره در دیتابیس
  build(overrides: Partial<User> = {}): Partial<User> {
    return {
      name:     faker.person.fullName(),
      email:    faker.internet.email(),
      age:      faker.number.int({ min: 18, max: 80 }),
      isActive: true,
      ...overrides,
    };
  }

  // ساخت و ذخیره در دیتابیس
  async create(overrides: Partial<User> = {}): Promise<User> {
    const repo = this.dataSource.getRepository(User);
    const user = repo.create(this.build(overrides));
    return repo.save(user);
  }

  // ساخت چند user یکجا
  async createMany(count: number, overrides: Partial<User> = {}): Promise<User[]> {
    return Promise.all(
      Array.from({ length: count }, () => this.create(overrides))
    );
  }

  // ساخت user با role خاص
  async createAdmin(): Promise<User> {
    return this.create({ role: 'admin', isActive: true });
  }
}
```

```typescript
// test/helpers/database.helper.ts
import { DataSource } from 'typeorm';

export class DatabaseHelper {
  constructor(private readonly dataSource: DataSource) {}

  // پاک کردن همه جداول به ترتیب درست (با رعایت foreign key)
  async cleanAll(): Promise<void> {
    const entities = this.dataSource.entityMetadatas;
    for (const entity of entities) {
      const repo = this.dataSource.getRepository(entity.name);
      await repo.query(`DELETE FROM "${entity.tableName}"`);
    }
  }

  // اجرای seed برای تست‌های خاص
  async seed(seedFn: (dataSource: DataSource) => Promise<void>): Promise<void> {
    await seedFn(this.dataSource);
  }
}
```

```typescript
// test/users.e2e-spec.ts — استفاده از Factory و Helper
describe('Users E2E با Factory', () => {
  let app: INestApplication;
  let userFactory: UserFactory;
  let dbHelper: DatabaseHelper;

  beforeAll(async () => {
    // ... راه‌اندازی app
    const dataSource = app.get(DataSource);
    userFactory = new UserFactory(dataSource);
    dbHelper    = new DatabaseHelper(dataSource);
  });

  beforeEach(async () => {
    await dbHelper.cleanAll(); // قبل از هر تست پاک می‌کنیم
  });

  it('باید لیست کاربران را با pagination برگرداند', async () => {
    // Arrange: ۱۵ کاربر می‌سازیم
    await userFactory.createMany(15);

    // Act
    const response = await request(app.getHttpServer())
      .get('/users?page=1&limit=10')
      .expect(200);

    // Assert
    expect(response.body.data).toHaveLength(10);
    expect(response.body.total).toBe(15);
    expect(response.body.page).toBe(1);
  });

  it('باید فقط کاربران active را برگرداند', async () => {
    await userFactory.createMany(3, { isActive: true });
    await userFactory.createMany(2, { isActive: false });

    const response = await request(app.getHttpServer())
      .get('/users?active=true')
      .expect(200);

    expect(response.body).toHaveLength(3);
    expect(response.body.every((u: User) => u.isActive)).toBe(true);
  });
});
```

---

### تست Cron Jobs با @nestjs/schedule

```typescript
// src/tasks/cleanup.task.ts
import { Injectable } from '@nestjs/common';
import { Cron, CronExpression } from '@nestjs/schedule';
import { UsersService } from '../users/users.service';

@Injectable()
export class CleanupTask {
  constructor(private readonly usersService: UsersService) {}

  @Cron(CronExpression.EVERY_DAY_AT_MIDNIGHT)
  async handleCleanup(): Promise<void> {
    const count = await this.usersService.removeInactiveUsers();
    console.log(`${count} کاربر غیرفعال حذف شدند`);
  }
}
```

```typescript
// src/tasks/cleanup.task.spec.ts
import { Test } from '@nestjs/testing';
import { CleanupTask } from './cleanup.task';
import { UsersService } from '../users/users.service';

describe('CleanupTask', () => {
  let task: CleanupTask;
  let usersService: jest.Mocked<UsersService>;

  beforeEach(async () => {
    const mockUsersService = {
      removeInactiveUsers: jest.fn(),
    };

    const module = await Test.createTestingModule({
      providers: [
        CleanupTask,
        { provide: UsersService, useValue: mockUsersService },
      ],
    }).compile();

    task         = module.get<CleanupTask>(CleanupTask);
    usersService = module.get(UsersService);
  });

  it('باید کاربران غیرفعال را حذف کند', async () => {
    usersService.removeInactiveUsers.mockResolvedValue(5);
    jest.spyOn(console, 'log').mockImplementation(() => {});

    await task.handleCleanup();

    expect(usersService.removeInactiveUsers).toHaveBeenCalledTimes(1);
    expect(console.log).toHaveBeenCalledWith('5 کاربر غیرفعال حذف شدند');
  });

  it('باید خطا را handle کند', async () => {
    usersService.removeInactiveUsers.mockRejectedValue(new Error('DB Error'));

    await expect(task.handleCleanup()).rejects.toThrow('DB Error');
  });
});
```

```typescript
// تست Integration — بررسی اینکه Cron واقعاً اجرا می‌شود
import { ScheduleModule } from '@nestjs/schedule';

describe('CleanupTask Integration', () => {
  it('باید Cron job را register کند', async () => {
    const module = await Test.createTestingModule({
      imports:   [ScheduleModule.forRoot()],
      providers: [CleanupTask, { provide: UsersService, useValue: { removeInactiveUsers: jest.fn() } }],
    }).compile();

    const schedulerRegistry = module.get(SchedulerRegistry);
    // بررسی اینکه cron job ثبت شده
    expect(() => schedulerRegistry.getCronJob('handleCleanup')).not.toThrow();
  });
});
```

---

### Mock کردن Third-Party Services

وقتی با سرویس‌های خارجی مثل Stripe، SendGrid یا AWS کار می‌کنید، هرگز نباید در تست به API واقعی وصل شوید.

```typescript
// ── مثال ۱: Mock کردن Stripe ──────────────────────────────

// src/payments/payments.service.ts
import Stripe from 'stripe';

@Injectable()
export class PaymentsService {
  constructor(private readonly stripe: Stripe) {}

  async createPaymentIntent(amount: number, currency: string) {
    return this.stripe.paymentIntents.create({ amount, currency });
  }

  async refund(paymentIntentId: string) {
    return this.stripe.refunds.create({ payment_intent: paymentIntentId });
  }
}
```

```typescript
// src/payments/payments.service.spec.ts
import Stripe from 'stripe';

// Mock کردن کل کتابخانه Stripe
jest.mock('stripe', () => {
  return jest.fn().mockImplementation(() => ({
    paymentIntents: {
      create: jest.fn(),
    },
    refunds: {
      create: jest.fn(),
    },
  }));
});

describe('PaymentsService', () => {
  let service: PaymentsService;
  let stripeMock: jest.Mocked<Stripe>;

  beforeEach(async () => {
    const StripeConstructor = require('stripe');
    stripeMock = new StripeConstructor() as jest.Mocked<Stripe>;

    const module = await Test.createTestingModule({
      providers: [
        PaymentsService,
        { provide: Stripe, useValue: stripeMock },
      ],
    }).compile();

    service = module.get<PaymentsService>(PaymentsService);
  });

  it('باید payment intent بسازد', async () => {
    const mockIntent = { id: 'pi_123', amount: 5000, status: 'requires_payment_method' };
    (stripeMock.paymentIntents.create as jest.Mock).mockResolvedValue(mockIntent);

    const result = await service.createPaymentIntent(5000, 'usd');

    expect(result).toEqual(mockIntent);
    expect(stripeMock.paymentIntents.create).toHaveBeenCalledWith({
      amount:   5000,
      currency: 'usd',
    });
  });

  it('باید refund انجام دهد', async () => {
    const mockRefund = { id: 're_123', amount: 5000, status: 'succeeded' };
    (stripeMock.refunds.create as jest.Mock).mockResolvedValue(mockRefund);

    const result = await service.refund('pi_123');

    expect(result).toEqual(mockRefund);
    expect(stripeMock.refunds.create).toHaveBeenCalledWith({ payment_intent: 'pi_123' });
  });
});
```

```typescript
// ── مثال ۲: Mock کردن SendGrid ────────────────────────────

jest.mock('@sendgrid/mail', () => ({
  setApiKey: jest.fn(),
  send:      jest.fn().mockResolvedValue([{ statusCode: 202 }]),
}));

import * as sgMail from '@sendgrid/mail';

describe('EmailService', () => {
  it('باید ایمیل بفرستد', async () => {
    await service.sendWelcomeEmail('user@test.com', 'Ali');

    expect(sgMail.send).toHaveBeenCalledWith(
      expect.objectContaining({
        to:      'user@test.com',
        subject: expect.stringContaining('خوش آمدید'),
      })
    );
  });

  it('باید خطای SendGrid را handle کند', async () => {
    (sgMail.send as jest.Mock).mockRejectedValue(new Error('API Error'));

    await expect(service.sendWelcomeEmail('user@test.com', 'Ali'))
      .rejects.toThrow('API Error');
  });
});
```

```typescript
// ── مثال ۳: Mock کردن AWS S3 ──────────────────────────────

jest.mock('@aws-sdk/client-s3', () => ({
  S3Client:        jest.fn().mockImplementation(() => ({ send: jest.fn() })),
  PutObjectCommand: jest.fn(),
  GetObjectCommand: jest.fn(),
}));

describe('StorageService', () => {
  it('باید فایل آپلود کند', async () => {
    const { S3Client } = require('@aws-sdk/client-s3');
    const mockSend = jest.fn().mockResolvedValue({ ETag: '"abc123"' });
    S3Client.mockImplementation(() => ({ send: mockSend }));

    const result = await service.uploadFile('test.jpg', Buffer.from('data'));

    expect(mockSend).toHaveBeenCalledTimes(1);
    expect(result.key).toBeDefined();
  });
});
```

---

### CI/CD Integration با GitHub Actions

```yaml
# .github/workflows/test.yml
name: Tests

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  unit-tests:
    name: Unit Tests
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run unit tests with coverage
        run: npm run test:cov

      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v4
        with:
          token: ${{ secrets.CODECOV_TOKEN }}
          files: ./coverage/lcov.info

  e2e-tests:
    name: E2E Tests
    runs-on: ubuntu-latest

    services:
      # دیتابیس PostgreSQL برای E2E
      postgres:
        image: postgres:16
        env:
          POSTGRES_USER:     test_user
          POSTGRES_PASSWORD: test_pass
          POSTGRES_DB:       test_db
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

      # Redis برای Queue
      redis:
        image: redis:7
        ports:
          - 6379:6379

    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run E2E tests
        run: npm run test:e2e
        env:
          DB_HOST:     localhost
          DB_PORT:     5432
          DB_USER:     test_user
          DB_PASSWORD: test_pass
          DB_NAME:     test_db
          REDIS_HOST:  localhost
          REDIS_PORT:  6379
          JWT_SECRET:  ci-test-secret
```

```json
// package.json — اضافه کردن script های مفید
{
  "scripts": {
    "test":          "jest",
    "test:watch":    "jest --watch",
    "test:cov":      "jest --coverage",
    "test:e2e":      "jest --config ./test/jest-e2e.json",
    "test:ci":       "jest --ci --coverage --runInBand",
    "test:e2e:ci":   "jest --config ./test/jest-e2e.json --ci --runInBand"
  }
}
```

> 💡 **نکته CI** — در محیط CI از `--runInBand` استفاده کنید تا تست‌ها به صورت sequential اجرا شوند. این از race condition در دیتابیس جلوگیری می‌کند. همچنین `--ci` باعث می‌شود Jest در صورت fail شدن snapshot، خودکار آن را update نکند.

---

## سطح ۶ — عمق بیشتر

### useValue vs useFactory vs useClass در TestingModule

این سه روش برای inject کردن dependency در TestingModule تفاوت‌های مهمی دارند:

```typescript
describe('تفاوت روش‌های provide', () => {

  // ── useValue: یک object آماده inject می‌کند ──────────────
  // بهترین برای: mock های ساده، object های ثابت
  const module1 = await Test.createTestingModule({
    providers: [
      {
        provide:  UsersService,
        useValue: {
          findAll: jest.fn().mockResolvedValue([]),
          findOne: jest.fn(),
        },
      },
    ],
  }).compile();

  // ── useFactory: یک factory function اجرا می‌کند ──────────
  // بهترین برای: وقتی به dependency های دیگر نیاز دارید
  // یا وقتی mock باید async باشد
  const module2 = await Test.createTestingModule({
    providers: [
      ConfigService,
      {
        provide:    DatabaseService,
        useFactory: (configService: ConfigService) => ({
          // می‌توانید از configService استفاده کنید
          connect: jest.fn().mockResolvedValue(
            configService.get('DB_URL')
          ),
        }),
        inject: [ConfigService], // dependency های factory را مشخص کنید
      },
    ],
  }).compile();

  // ── useClass: یک class جایگزین inject می‌کند ─────────────
  // بهترین برای: وقتی یک implementation جایگزین دارید
  class MockEmailService implements EmailService {
    async send() { return true; }
    async sendBulk() { return []; }
  }

  const module3 = await Test.createTestingModule({
    providers: [
      {
        provide:  EmailService,   // interface یا class اصلی
        useClass: MockEmailService, // پیاده‌سازی جایگزین
      },
    ],
  }).compile();
});
```

```typescript
// ── مثال واقعی: useFactory با async ──────────────────────

const module = await Test.createTestingModule({
  providers: [
    {
      provide:    'REDIS_CLIENT',
      useFactory: async () => {
        // می‌توانید async کار کنید
        const client = createClient({ url: 'redis://localhost:6379' });
        await client.connect();
        return client;
      },
    },
    CacheService,
  ],
}).compile();

// ── مثال واقعی: useFactory با چند dependency ─────────────

const module = await Test.createTestingModule({
  providers: [
    ConfigService,
    JwtService,
    {
      provide:    AuthService,
      useFactory: (config: ConfigService, jwt: JwtService) => {
        return new AuthService(config, jwt);
      },
      inject: [ConfigService, JwtService],
    },
  ],
}).compile();
```

---

### Supertest پیشرفته — Headers، Cookies و فایل‌ها

```typescript
describe('Supertest پیشرفته', () => {

  // ── ارسال با Header سفارشی ────────────────────────────────
  it('باید با API key احراز هویت کند', async () => {
    await request(app.getHttpServer())
      .get('/api/data')
      .set('X-API-Key', 'my-secret-api-key')
      .set('Accept-Language', 'fa')
      .expect(200);
  });

  // ── کار با Cookie ─────────────────────────────────────────
  it('باید cookie را set و read کند', async () => {
    // Login و گرفتن cookie
    const loginRes = await request(app.getHttpServer())
      .post('/auth/login')
      .send({ email: 'user@test.com', password: 'pass123' })
      .expect(200);

    const cookies = loginRes.headers['set-cookie'];

    // استفاده از cookie در request بعدی
    const profileRes = await request(app.getHttpServer())
      .get('/profile')
      .set('Cookie', cookies)
      .expect(200);

    expect(profileRes.body.email).toBe('user@test.com');
  });

  // ── آپلود فایل ────────────────────────────────────────────
  it('باید فایل آپلود کند', async () => {
    const response = await request(app.getHttpServer())
      .post('/upload')
      .set('Authorization', `Bearer ${accessToken}`)
      .attach('file', Buffer.from('file content'), {
        filename:    'test.txt',
        contentType: 'text/plain',
      })
      .field('description', 'فایل تستی')
      .expect(201);

    expect(response.body.filename).toBe('test.txt');
    expect(response.body.size).toBeGreaterThan(0);
  });

  // ── بررسی Response Headers ────────────────────────────────
  it('باید header های امنیتی داشته باشد', async () => {
    const response = await request(app.getHttpServer())
      .get('/users')
      .expect(200);

    expect(response.headers['x-content-type-options']).toBe('nosniff');
    expect(response.headers['x-frame-options']).toBeDefined();
    expect(response.headers['content-type']).toMatch(/application\/json/);
  });

  // ── تست Redirect ──────────────────────────────────────────
  it('باید به URL جدید redirect کند', async () => {
    const response = await request(app.getHttpServer())
      .get('/old-endpoint')
      .redirects(0) // دنبال redirect نرو
      .expect(301);

    expect(response.headers['location']).toBe('/new-endpoint');
  });

  // ── تست با Query Parameters پیچیده ───────────────────────
  it('باید با filter و sort کار کند', async () => {
    await userFactory.createMany(5, { isActive: true });
    await userFactory.createMany(3, { isActive: false });

    const response = await request(app.getHttpServer())
      .get('/users')
      .query({ active: true, sort: 'name', order: 'asc', limit: 3 })
      .expect(200);

    expect(response.body).toHaveLength(3);
    // بررسی مرتب‌سازی
    const names = response.body.map((u: User) => u.name);
    expect(names).toEqual([...names].sort());
  });
});
```

---

### Snapshot Testing

Snapshot Testing برای بررسی اینکه خروجی یک تابع یا component تغییر نکرده مفید است:

```typescript
describe('Snapshot Testing', () => {

  // ── Snapshot ساده ─────────────────────────────────────────
  it('باید response ثابت داشته باشد', async () => {
    const user = await userFactory.create({
      id:    1,
      name:  'Ali Ahmadi',
      email: 'ali@test.com',
      age:   25,
    });

    const response = await request(app.getHttpServer())
      .get(`/users/${user.id}`)
      .expect(200);

    // اولین بار: snapshot می‌سازد
    // بعد از آن: با snapshot قبلی مقایسه می‌کند
    expect(response.body).toMatchSnapshot();
  });

  // ── Inline Snapshot ───────────────────────────────────────
  it('باید error response ثابت داشته باشد', async () => {
    const response = await request(app.getHttpServer())
      .get('/users/99999')
      .expect(404);

    expect(response.body).toMatchInlineSnapshot(`
      {
        "message": "User with id 99999 not found",
        "statusCode": 404,
      }
    `);
  });

  // ── Snapshot با serializer سفارشی ────────────────────────
  // برای حذف فیلدهای dynamic مثل timestamp و id
  it('باید ساختار user را بررسی کند', async () => {
    const user = await userFactory.create();

    const response = await request(app.getHttpServer())
      .get(`/users/${user.id}`)
      .expect(200);

    // حذف فیلدهای dynamic قبل از snapshot
    const { id, createdAt, updatedAt, ...stableFields } = response.body;

    expect(stableFields).toMatchSnapshot();
  });
});
```

```typescript
// ── Snapshot برای DTO/Serializer ─────────────────────────

describe('UserSerializer Snapshot', () => {
  it('باید user را با فرمت درست serialize کند', () => {
    const user: User = {
      id:       1,
      name:     'Ali Ahmadi',
      email:    'ali@test.com',
      age:      25,
      isActive: true,
    };

    const serialized = new UserSerializer(user).toJSON();

    expect(serialized).toMatchSnapshot();
    // snapshot ذخیره می‌شود در __snapshots__/users.spec.ts.snap
  });
});
```

> 💡 **آپدیت Snapshot** — وقتی عمداً خروجی را تغییر دادید، با `npx jest --updateSnapshot` یا `npx jest -u` snapshot ها را آپدیت کنید.

---

### تست WebSocket Gateway

```typescript
// src/chat/chat.gateway.ts
import { WebSocketGateway, SubscribeMessage, MessageBody, ConnectedSocket } from '@nestjs/websockets';
import { Socket } from 'socket.io';

@WebSocketGateway({ namespace: '/chat' })
export class ChatGateway {
  @SubscribeMessage('sendMessage')
  handleMessage(
    @MessageBody() data: { room: string; message: string },
    @ConnectedSocket() client: Socket,
  ) {
    client.to(data.room).emit('newMessage', {
      message: data.message,
      from:    client.id,
    });
    return { status: 'sent' };
  }

  @SubscribeMessage('joinRoom')
  handleJoinRoom(
    @MessageBody() room: string,
    @ConnectedSocket() client: Socket,
  ) {
    client.join(room);
    return { joined: room };
  }
}
```

```typescript
// src/chat/chat.gateway.spec.ts — Unit Test
import { ChatGateway } from './chat.gateway';
import { Socket } from 'socket.io';

describe('ChatGateway Unit', () => {
  let gateway: ChatGateway;
  let mockSocket: Partial<Socket>;

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [ChatGateway],
    }).compile();

    gateway = module.get<ChatGateway>(ChatGateway);

    mockSocket = {
      id:   'socket-123',
      to:   jest.fn().mockReturnThis(),
      emit: jest.fn(),
      join: jest.fn(),
    };
  });

  it('باید پیام را به room بفرستد', () => {
    const data = { room: 'room-1', message: 'سلام' };

    const result = gateway.handleMessage(data, mockSocket as Socket);

    expect(mockSocket.to).toHaveBeenCalledWith('room-1');
    expect(mockSocket.emit).toHaveBeenCalledWith('newMessage', {
      message: 'سلام',
      from:    'socket-123',
    });
    expect(result).toEqual({ status: 'sent' });
  });

  it('باید به room بپیوندد', () => {
    const result = gateway.handleJoinRoom('room-1', mockSocket as Socket);

    expect(mockSocket.join).toHaveBeenCalledWith('room-1');
    expect(result).toEqual({ joined: 'room-1' });
  });
});
```

```typescript
// test/chat.e2e-spec.ts — E2E Test با socket.io-client
import { io, Socket as ClientSocket } from 'socket.io-client';

describe('ChatGateway E2E', () => {
  let app: INestApplication;
  let clientSocket1: ClientSocket;
  let clientSocket2: ClientSocket;

  beforeAll(async () => {
    const moduleFixture = await Test.createTestingModule({
      imports: [ChatModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.listen(0); // پورت تصادفی
  });

  beforeEach((done) => {
    const port = (app.getHttpServer().address() as any).port;
    const url  = `http://localhost:${port}/chat`;

    clientSocket1 = io(url);
    clientSocket2 = io(url);

    // صبر می‌کنیم هر دو connect شوند
    let connected = 0;
    const onConnect = () => { if (++connected === 2) done(); };
    clientSocket1.on('connect', onConnect);
    clientSocket2.on('connect', onConnect);
  });

  afterEach(() => {
    clientSocket1.disconnect();
    clientSocket2.disconnect();
  });

  afterAll(async () => {
    await app.close();
  });

  it('باید پیام را به client دیگر در همان room برساند', (done) => {
    // client2 به room می‌پیوندد
    clientSocket2.emit('joinRoom', 'test-room');

    // client2 منتظر پیام می‌ماند
    clientSocket2.on('newMessage', (data) => {
      expect(data.message).toBe('سلام دنیا');
      done();
    });

    // کمی صبر می‌کنیم تا join کامل شود
    setTimeout(() => {
      clientSocket1.emit('joinRoom', 'test-room');
      setTimeout(() => {
        clientSocket1.emit('sendMessage', {
          room:    'test-room',
          message: 'سلام دنیا',
        });
      }, 50);
    }, 50);
  });

  it('باید acknowledgment برگرداند', (done) => {
    clientSocket1.emit('joinRoom', 'room-x', (response: any) => {
      expect(response).toEqual({ joined: 'room-x' });
      done();
    });
  });
});
```

---

<div align="center">

ساخته شده با ❤️ — [مشاهده ریپو در GitHub](https://github.com/irzix/nestjs-testing-course/)
##### علیرضا محققی - Alireza Mohagheghi


</div>

</div>
