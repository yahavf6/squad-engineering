# Frontend Boilerplate Example

This example demonstrates a typical frontend squad role setup for a React + TypeScript application.

## Example Structure

```
frontend-app/
├── src/
│   ├── components/
│   │   ├── common/
│   │   └── features/
│   ├── hooks/
│   ├── utils/
│   ├── types/
│   └── App.tsx
├── tests/
├── package.json
└── tsconfig.json
```

## Example Role Plan for Frontend Developer

### Tech Stack
- React 18.x
- TypeScript 5.x
- Vite
- Tailwind CSS
- Vitest + React Testing Library

### Typical Tasks
1. Create reusable UI components
2. Implement responsive layouts
3. Add interactive features
4. Write component tests
5. Ensure accessibility standards

### Conventions
- Functional components only
- Custom hooks for logic extraction
- Atomic commits
- Mobile-first responsive design
- ARIA labels for accessibility

## Sample Component

```typescript
// Button.tsx
import React from 'react';

interface ButtonProps {
  onClick: () => void;
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
}

export const Button: React.FC<ButtonProps> = ({ 
  onClick, 
  children, 
  variant = 'primary',
  disabled = false 
}) => {
  const baseClasses = "px-4 py-2 rounded-md font-medium transition-colors";
  const variantClasses = {
    primary: "bg-blue-600 text-white hover:bg-blue-700",
    secondary: "bg-gray-200 text-gray-800 hover:bg-gray-300"
  };
  
  return (
    <button
      onClick={onClick}
      disabled={disabled}
      className={`${baseClasses} ${variantClasses[variant]} ${
        disabled ? 'opacity-50 cursor-not-allowed' : ''
      }`}
      aria-label={typeof children === 'string' ? children : undefined}
    >
      {children}
    </button>
  );
};
```

## Sample Test

```typescript
// Button.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  it('renders children correctly', () => {
    render(<Button onClick={() => {}}>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    fireEvent.click(screen.getByText('Click me'));
    expect(handleClick).toHaveBeenCalledOnce();
  });

  it('is disabled when disabled prop is true', () => {
    render(<Button onClick={() => {}} disabled>Click me</Button>);
    expect(screen.getByText('Click me')).toBeDisabled();
  });
});
```

## Integration with Squad Engineering

When a frontend developer role is generated, they would:
1. Use this boilerplate as a reference
2. Follow the established patterns
3. Maintain consistency across components
4. Ensure all components have tests
5. Document props and usage