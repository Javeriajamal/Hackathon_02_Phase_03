# Phase-3 MCP Tools Specification — Todo Chatbot

**Created**: 2026-02-02
**Status**: Draft
**Target Audience**: Hackathon evaluators and reviewers assessing tool correctness, determinism, and agent safety

## 1. Overview & Purpose

The MCP (Model Context Protocol) tools specification defines standardized contracts for the AI agent to interact with the Phase-2 todo management system. These tools provide a stateless, deterministic interface for managing todo items through well-defined input/output patterns. The tools enable the AI agent to perform core todo operations while maintaining auditability, safety, and consistency with the Phase-3 functional specification.

Each tool follows a strict contract ensuring predictable behavior, clear error reporting, and safe agent operation within defined boundaries.

## 2. Tool Design Principles

- **Deterministic Behavior**: Each tool produces consistent outputs for identical inputs
- **Statelessness**: Tools do not maintain session state between invocations
- **Auditable Operations**: All tool usage generates clear logs for monitoring and debugging
- **Safe Execution**: Tools include built-in safeguards against invalid operations
- **Clear Contract Boundaries**: Well-defined inputs, outputs, and error cases
- **Idempotent Operations**: Safe to retry operations without unintended side effects where applicable

## 3. Tool Specifications

### add_task

#### Purpose
Creates a new todo item in the user's task list with specified properties and metadata.

#### Required inputs
- `title`: String representing the task content/description
- `user_id`: Identifier for the user owning the task

#### Optional inputs
- `description`: Additional details about the task
- `priority`: Priority level (low, medium, high)
- `due_date`: Expected completion date/time
- `category`: Category classification for the task
- `tags`: Array of string tags for organization

#### Outputs
- `task_id`: Unique identifier for the created task
- `created_at`: Timestamp of task creation
- `status`: Current status of the task (active)

#### Side effects
- New task record is persisted in the database
- Task becomes accessible through other tools

#### Error cases
- `INVALID_INPUT`: Missing required fields or invalid data types
- `USER_NOT_FOUND`: Provided user_id does not exist
- `QUOTA_EXCEEDED`: User has reached maximum allowed tasks
- `DATABASE_ERROR`: Failure to persist the task

---

### list_tasks

#### Purpose
Retrieves a filtered list of tasks for a specific user based on specified criteria.

#### Required inputs
- `user_id`: Identifier for the user whose tasks to retrieve

#### Optional inputs
- `status_filter`: Filter by task status (active, completed, all)
- `category_filter`: Filter by task category
- `priority_filter`: Filter by priority level
- `limit`: Maximum number of tasks to return
- `offset`: Number of tasks to skip for pagination
- `sort_by`: Field to sort results by (created_at, due_date, priority)

#### Outputs
- `tasks`: Array of task objects containing id, title, status, priority, due_date, category, tags, created_at
- `total_count`: Total number of tasks matching the filters
- `filtered_count`: Number of tasks in the returned array

#### Side effects
- None

#### Error cases
- `INVALID_USER_ID`: Provided user_id is malformed
- `USER_NOT_FOUND`: Provided user_id does not exist
- `INVALID_FILTER`: Provided filter parameters are invalid
- `DATABASE_ERROR`: Failure to retrieve tasks

---

### complete_task

#### Purpose
Marks a specific task as completed, changing its status and recording completion time.

#### Required inputs
- `task_id`: Unique identifier of the task to complete
- `user_id`: Identifier for the user attempting to complete the task

#### Optional inputs
- `completion_notes`: Optional notes about task completion
- `actual_completion_time`: Specific timestamp for completion (defaults to current time)

#### Outputs
- `task_id`: Identifier of the completed task
- `previous_status`: Status before completion
- `completed_at`: Timestamp of completion
- `updated_status`: New status (completed)

#### Side effects
- Task status is updated to "completed" in the database
- Completion timestamp is recorded
- Task is no longer returned in active task lists

#### Error cases
- `TASK_NOT_FOUND`: Provided task_id does not exist
- `USER_MISMATCH`: User does not own the specified task
- `ALREADY_COMPLETED`: Task is already marked as completed
- `INVALID_TASK_ID`: Provided task_id is malformed
- `DATABASE_ERROR`: Failure to update the task

---

### delete_task

#### Purpose
Permanently removes a task from the user's task list and database.

#### Required inputs
- `task_id`: Unique identifier of the task to delete
- `user_id`: Identifier for the user attempting to delete the task

#### Optional inputs
- `reason`: Reason for deletion (for audit purposes)

#### Outputs
- `task_id`: Identifier of the deleted task
- `deleted_at`: Timestamp of deletion

#### Side effects
- Task record is permanently removed from the database
- Associated metadata and relationships are cleared

#### Error cases
- `TASK_NOT_FOUND`: Provided task_id does not exist
- `USER_MISMATCH`: User does not own the specified task
- `INVALID_TASK_ID`: Provided task_id is malformed
- `PERMISSION_DENIED`: User lacks permission to delete the task
- `DATABASE_ERROR`: Failure to delete the task

---

### update_task

#### Purpose
Modifies properties of an existing task while preserving its identity and relationships.

#### Required inputs
- `task_id`: Unique identifier of the task to update
- `user_id`: Identifier for the user attempting to update the task

#### Optional inputs
- `title`: New title for the task
- `description`: New description for the task
- `priority`: New priority level
- `due_date`: New due date/time
- `category`: New category classification
- `tags`: New array of tags
- `status`: New status (with validation)

#### Outputs
- `task_id`: Identifier of the updated task
- `updated_fields`: Object containing the fields that were changed
- `updated_at`: Timestamp of the update

#### Side effects
- Task record is updated in the database
- Change history may be maintained for audit purposes

#### Error cases
- `TASK_NOT_FOUND`: Provided task_id does not exist
- `USER_MISMATCH`: User does not own the specified task
- `INVALID_TASK_ID`: Provided task_id is malformed
- `INVALID_STATUS_CHANGE`: Attempt to change status to an invalid state
- `INVALID_INPUT`: Provided update values are invalid
- `DATABASE_ERROR`: Failure to update the task

## 4. Tool Usage Guarantees

- **Consistency**: All tools maintain data integrity and enforce business rules
- **Security**: Each tool validates user permissions before performing operations
- **Reliability**: Tools provide clear error messages and fail gracefully
- **Performance**: Tools operate within defined time limits and resource constraints
- **Audit Trail**: All tool invocations are logged with sufficient detail for debugging
- **Recoverability**: Failed operations do not leave data in inconsistent states
- **Compatibility**: Tools maintain backward compatibility with existing data structures

## 5. Explicit Exclusions

### Not Building
- Agent reasoning logic or decision-making algorithms
- Natural language processing or interpretation mechanisms
- User interface components or frontend behavior
- Database schema definitions or migration scripts
- Authentication protocols or session management
- Network communication protocols or transport layers
- Machine learning model training or inference
- Real-time notification systems
- File storage or media handling
- Third-party service integrations
- UI/UX design specifications
- Phase-4 or Phase-5 functionality concerns