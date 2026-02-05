# Phase-3 CLAUDE.md - AI-Powered Todo Management System

## Overview

This document provides guidelines for Claude when working on Phase-3 of the Evolution of Todo project. Phase-3 integrates an AI chatbot assistant into the existing todo management system, enabling natural language task management capabilities.

## Phase-3 Goals and Constraints

### Primary Objectives
- Integrate AI-powered natural language processing for task management
- Maintain consistency with existing Phase-1 and Phase-2 architecture
- Enhance user experience with intuitive chatbot interface
- Preserve all existing authentication and data integrity features

### Development Constraints
- Do NOT modify authentication systems without explicit permission
- Do NOT change backend API contracts without coordination
- Do NOT alter database schemas without approval
- Do NOT modify core todo management business logic
- Do NOT change routing structures without consultation
- Maintain backward compatibility with existing features

## Coding Discipline Rules

### Styling and UI Consistency
- Follow the existing dark-themed, neon cyberpunk design system
- Use Tailwind CSS utility classes consistently
- Apply glassmorphism effects (`glass` class) where appropriate
- Use neon glow effects (`neon-glow`, `neon-glow-purple`) for interactive elements
- Maintain proper color contrast ratios for accessibility

### TypeScript Standards
- Use strict TypeScript with explicit typing
- Follow existing interface and type definition patterns
- Maintain consistent error handling patterns
- Use React best practices for state management

### AI Integration Guidelines
- Preserve existing chatbot functionality and API contracts
- Follow established patterns for natural language processing
- Maintain proper error handling for API failures
- Respect rate limits and API usage constraints

## File Organization Principles

### Component Structure
- Place all chatbot-specific components in `frontend/components/chat/`
- Maintain separation between UI presentation and business logic
- Follow consistent naming conventions (PascalCase for components)
- Organize services by functionality in the `services/` directory

### Type Definitions
- Centralize TypeScript types in the `types/` directory
- Maintain consistency with existing type definitions
- Use descriptive names for interfaces and types
- Import types using absolute paths (`@/types/`)

## Safe Change Implementation

### Frontend Changes
- Always test UI changes across multiple browsers
- Verify responsive behavior on different screen sizes
- Maintain accessibility standards (ARIA labels, semantic HTML)
- Follow existing animation and transition patterns

### Backend Changes
- Preserve existing API endpoints and contracts
- Follow established database query patterns
- Maintain security best practices (input validation, sanitization)
- Update documentation when modifying APIs

### Chatbot Logic
- Do NOT modify core AI processing logic without approval
- Maintain existing tool call patterns and response formats
- Preserve conversation context and state management
- Follow established error recovery patterns

## Prohibited Actions Without Permission

Claude MUST NOT perform the following actions without explicit user permission:

1. **Authentication System Changes**
   - Modifying JWT token generation/validation
   - Changing password hashing algorithms
   - Altering user session management

2. **Database Schema Modifications**
   - Adding/removing/modifying collection structures
   - Changing field types or validation rules
   - Updating database connection configurations

3. **Core Business Logic**
   - Modifying todo creation, update, or deletion logic
   - Changing user permission systems
   - Altering data validation rules

4. **External API Integrations**
   - Changing OpenAI API integration patterns
   - Modifying third-party service connections
   - Updating API key handling mechanisms

5. **Deployment Configuration**
   - Modifying Docker configurations
   - Changing CI/CD pipeline settings
   - Updating environment variable handling

## Documentation and PHR Workflow

### Process History Records (PHRs)
- Create PHRs for all significant changes using the format: `Phase-3/history/prompts/[ID]-[title].[stage].prompt.md`
- Include detailed change descriptions and impact assessments
- Document testing procedures and validation results
- Maintain traceability between changes and requirements

### Code Comments
- Update comments when modifying functionality
- Document any deviations from established patterns
- Include reasoning for architectural decisions
- Maintain consistency with existing comment styles

## Quality Assurance Standards

### Testing Requirements
- Verify all changes maintain existing functionality
- Test chatbot interactions thoroughly
- Validate UI/UX changes across different themes
- Confirm authentication flows remain secure

### Performance Considerations
- Minimize API call overhead
- Optimize component rendering performance
- Consider mobile device performance implications
- Maintain reasonable load times for all features

## Emergency Procedures

If uncertain about any change:
1. ASK the user for clarification before proceeding
2. Reference existing code patterns and implementations
3. Consider impact on existing functionality
4. Document potential risks before implementation

Remember: When in doubt, ask for permission before modifying any core system components.