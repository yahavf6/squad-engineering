# Backend Boilerplate Example

This example demonstrates a typical backend squad role setup for a Node.js + Express API.

## Example Structure

```
backend-api/
├── src/
│   ├── controllers/
│   ├── services/
│   ├── models/
│   ├── middleware/
│   ├── routes/
│   ├── utils/
│   └── app.ts
├── tests/
│   ├── unit/
│   └── integration/
├── package.json
└── tsconfig.json
```

## Example Role Plan for Backend Developer

### Tech Stack
- Node.js 18.x
- Express 4.x
- TypeScript 5.x
- PostgreSQL / MongoDB
- Jest for testing

### Typical Tasks
1. Create RESTful API endpoints
2. Implement business logic
3. Set up database models
4. Add authentication/authorization
5. Write unit and integration tests

### Conventions
- RESTful API design
- Layered architecture (controller → service → model)
- Error handling middleware
- Input validation
- Comprehensive logging

## Sample Controller

```typescript
// userController.ts
import { Request, Response, NextFunction } from 'express';
import { UserService } from '../services/userService';
import { CreateUserDto } from '../dtos/user.dto';
import { validateDto } from '../utils/validation';

export class UserController {
  constructor(private userService: UserService) {}

  async createUser(req: Request, res: Response, next: NextFunction) {
    try {
      const createUserDto = await validateDto(CreateUserDto, req.body);
      const user = await this.userService.create(createUserDto);
      
      res.status(201).json({
        status: 'success',
        data: { user }
      });
    } catch (error) {
      next(error);
    }
  }

  async getUser(req: Request, res: Response, next: NextFunction) {
    try {
      const { id } = req.params;
      const user = await this.userService.findById(id);
      
      if (!user) {
        return res.status(404).json({
          status: 'error',
          message: 'User not found'
        });
      }
      
      res.json({
        status: 'success',
        data: { user }
      });
    } catch (error) {
      next(error);
    }
  }

  async updateUser(req: Request, res: Response, next: NextFunction) {
    try {
      const { id } = req.params;
      const updateData = await validateDto(UpdateUserDto, req.body);
      const user = await this.userService.update(id, updateData);
      
      res.json({
        status: 'success',
        data: { user }
      });
    } catch (error) {
      next(error);
    }
  }
}
```

## Sample Service

```typescript
// userService.ts
import { User } from '../models/user.model';
import { CreateUserDto, UpdateUserDto } from '../dtos/user.dto';
import { AppError } from '../utils/errors';

export class UserService {
  async create(data: CreateUserDto): Promise<User> {
    // Check if user already exists
    const existingUser = await User.findByEmail(data.email);
    if (existingUser) {
      throw new AppError('User already exists', 400);
    }
    
    // Create new user
    const user = await User.create({
      ...data,
      // Hash password, etc.
    });
    
    return user;
  }

  async findById(id: string): Promise<User | null> {
    return User.findById(id);
  }

  async update(id: string, data: UpdateUserDto): Promise<User> {
    const user = await User.findByIdAndUpdate(id, data, { new: true });
    if (!user) {
      throw new AppError('User not found', 404);
    }
    return user;
  }
}
```

## Sample Test

```typescript
// userService.test.ts
import { UserService } from '../userService';
import { User } from '../../models/user.model';

jest.mock('../../models/user.model');

describe('UserService', () => {
  let userService: UserService;

  beforeEach(() => {
    userService = new UserService();
    jest.clearAllMocks();
  });

  describe('create', () => {
    it('should create a new user', async () => {
      const userData = {
        email: 'test@example.com',
        name: 'Test User'
      };

      User.findByEmail = jest.fn().mockResolvedValue(null);
      User.create = jest.fn().mockResolvedValue({ id: '1', ...userData });

      const user = await userService.create(userData);

      expect(User.findByEmail).toHaveBeenCalledWith(userData.email);
      expect(User.create).toHaveBeenCalledWith(userData);
      expect(user).toEqual({ id: '1', ...userData });
    });

    it('should throw error if user already exists', async () => {
      User.findByEmail = jest.fn().mockResolvedValue({ id: '1' });

      await expect(userService.create({ 
        email: 'existing@example.com',
        name: 'Existing User'
      })).rejects.toThrow('User already exists');
    });
  });
});
```

## Integration with Squad Engineering

When a backend developer role is generated, they would:
1. Use this boilerplate as a reference
2. Follow the layered architecture pattern
3. Implement comprehensive error handling
4. Write tests for all endpoints
5. Document API endpoints