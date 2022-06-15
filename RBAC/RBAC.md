# RBAC

It stands for Role-Based Access Control.

`RBAC` is the idea of assigning system access to users based on their role in an organization. It's important to remember that not every employee needs a starring role.

## Benefits of RBAC

The assignment of access rights becomes systematic and repeatable.

It is much easier to audit user rights.

And to correct any issues identified.

Will make the ongoing management of access rights much easier and more secure.

## Access control lists (ACL)

An ACL is a means of defining access rights by a given user or user group, to a specific object, such as a document. As a simple example, an ACL could be used to allow users from one department to make changes to a document, while only allowing users from other departments to read the document.

## Attribute-based access control (ABAC)

> policy-based access control.

can use a variety of attributes, including user department, time of day, location of access, type of access required, etc. to determine whether a user’s access request should be granted.

## RBAC implementation

1. Inventory your systems
   > Examples: email system, customer database, contact management system, major folders on a file server, etc.
2. Analyze your workforce and create roles
   > Examples: basic user role, a customer service rep and a customer database administrator.
3. Assign people to roles

4. Never make one-off changes

5. Audit

## Three primary rules are defined for RBAC:

1. Role assignment

2. Role authorization

3. Permission authorization

- A subject can have multiple roles.
- A role can have multiple subjects.
- A role can have many permissions.
- A permission can be assigned to many roles.
- An operation can be assigned to many permissions.
- A permission can be assigned to many operations.
