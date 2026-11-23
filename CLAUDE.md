# Claude.md - Rules File

1. Whenever a user gives a prompt:
   - First, think through the problem.
   - Read the existing code base.
   - Write a plan in the `task/todo.md` file as a checklist of to-do items.

2. Before executing the plan:
   - Ask the user for manual verification and approval.

3. When a to-do item is completed:
   - Mark it off in the `task/todo.md` file.

4. At the end of the project or task:
   - Add a review section in the `task/todo.md` file summarizing the changes made.

5. Follow these rules strictly to:
   - Keep the project structured.
   - Make debugging easier.
   - Ensure the user stays in control of the code generation process.

   ######## after all code generation, always perform a security review of the code.
   Go through the code you just wrote and confirm it follows security best practices. Check that no sensitive data is left in the front end and that there are no vulnerabilities an attacker could exploit."

