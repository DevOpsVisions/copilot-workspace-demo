# Common Conventions and Standards
This document provides guidance on common conventions and standards, including examples but without specific values. For precise conventions and values, please refer to the detailed guidelines within each individual project and repository.

## Repository and Application

This section outlines the objects that should standardized naming conventions used throughout all projects to maintain consistency and clarity:

- **Repository Name**: The full, descriptive name for the project repository, reflecting its purpose.
- **Application Name**: The concise, user-friendly name for the application, ideal for branding and communication.
- **Executable Name**: The short and efficient name used for the executable file, optimized for easy reference in scripts and command-line usage.

## Solution and Projects

To maintain a structured and organized codebase, the following naming conventions are used for the solution and project files:

- **Solution File**: The overarching solution file that includes all related projects.
- **Project Files**:
  - One main project file for the core application.
  - One project file dedicated to unit tests.
  - One project file dedicated to integration tests.

## Azure Cloud

A well-structured naming convention for Azure resources is crucial for quickly identifying the resource type, associated workload, environment, Azure region, and instance. Our naming convention follows these key elements:

### Example:

- **Resource Type:** `vm`, `st`, `appsvc`, `sql`, `nsg`, `kv`, `rg`, `pip`, `aks`, `lb`
- **Workload/Application:** `webapp`, `api`, `hrportal`, `crm`, `salesdata`, `logs`
- **Environment:** `prod`, `dev`, `test`, `staging`, `qa`, `uat`
- **Azure Region:** `eastus`, `westeurope`, `centralus`, `westus2`, `southeastasia`, `uksouth`
- **Instance:** `001`, `002`, `003`, `004`, `005`


More info: [Microsoft Azure Docs](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)

## Repository Folder Structure

The following is the folder structure used within the repository to maintain a clear and organized layout:

### Folder Structure and Descriptions for App Repos

- **/docs**: Contains all documentation related to the project.
  - **/standards-and-practices**: Holds documents outlining the standards and practices followed in the project.
  - **/technical-guides**: Contains guides for deploying and managing the project, like `deploy-q2a-azure-vm.md`.
  
- **/src**: The source code directory.
  - **/app**: Holds the application code.
  - **/iac**: Infrastructure as Code (IaC) files for setting up the environment.


### Folder Structure and Descriptions for DB Repos

- **/docs**: Contains all documentation related to the project.
  - **/standards-and-practices**: Holds documents outlining the standards and practices followed in the project.
  - **/technical-guides**: Contains guides for deploying and managing the project, including database-related guides.

- **/src**: The source code directory.
  - **/db**: Contains all database-related files.
    - **/schemas**: Holds database schema definition files, such as table structures, relationships, and indexes.
    - **/stored_procedures**: Contains stored procedure scripts that encapsulate business logic.
    - **/functions**: Contains scripts for database functions, including scalar and table-valued functions.
    - **/views**: Holds SQL scripts that define database views.
    - **/triggers**: Contains scripts for database triggers, such as after/insert/update/delete triggers.
    - **/migrations**: Contains migration scripts for handling schema changes, versioning, and updates to the database.
    - **/scripts**: Contains additional SQL scripts or utility scripts that do not fit into other specific categories.
    - **/seed_data**: Holds data seeding scripts for populating the database with initial or test data.
    - **/backups**: Contains database backup files. (Ensure sensitive information is handled appropriately.)
    - **/config**: Holds configuration files related to database connections, environment settings, or other relevant configurations.
    - **/indexes**: Contains SQL scripts for defining indexes used in the database.
    - **/constraints**: Holds scripts for defining constraints, such as primary keys, foreign keys, and unique constraints.

  - **/iac**: Infrastructure as Code (IaC) files for setting up the environment, including database provisioning and configuration scripts.



## Release Notes Template 
The following is the release note template used to organize key details of a product update, including release date, developer info, version, new features, bug fixes, and downloadable assets. It ensures clear communication of changes to users.

|<p>**Date**</p><p>**@Develper account**</p><p> **Tag**</p><p> **Commit** <br />&nbsp;<br /> <br />&nbsp;<br /><br />&nbsp;<br /><br />&nbsp;<br /><br />&nbsp;<br /><br />&nbsp;<br />  </p>|<p>**Product Name version** </p><p> (Org name/link) released from (n) days ago &nbsp; &nbsp; (tag) &nbsp; &nbsp; &nbsp; &nbsp; (commit) </p><p></p><p> Version (Release Date)</p><p></p><p>**Features Added:**</p><p>- Issue Title (Issue ID, PR ID) </p><p></p><p>**Bugs Fixed:**</p><p>- Issue Title (Issue ID, PR ID) </p><p></p><p>**Assets**</p><p> App (zip)	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Date </p><p> Source code (zip) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Date</p><p></p>|
| :- | :- |

## Kebab Case
By adopting the kebab case for URLs, file names, Azure resources, and GitHub repositories, the projects maintain clarity and uniformity across different web assets, cloud infrastructure, and code repositories, improving both collaboration and readability.
- **Purpose**: Kebab case is used to enhance readability and maintain uniformity in naming conventions. This format, which uses lowercase letters and hyphens to separate words (e.g., `project-name`, `user-profile`), is applied consistently across multiple contexts.

- **Use Cases Relevant to Our Projects**:
  - **URLs and Slugs**: Clean, SEO-friendly URLs (e.g., `https://example.com/user-profile/settings`).
  - **File Names**: Consistently formatted file names across different environments, ensuring clarity and ease of management (`data-fetching-service.js`).
  - **Folder Names**: All folder names (e.g., `project-assets`, `user-profiles`), providing a consistent approach to organizing directories in both local and cloud environments.
  - **Azure Resources**: All Azure resource names (such as storage accounts, databases, and resource groups) will follow the kebab case convention (e.g., `my-storage-account`), aligning with Azure's naming guidelines for easier resource identification and management.
  - **GitHub Repositories**: Repository names on GitHub will use kebab case (e.g., `project-management-tool`), providing consistency across version control and collaboration efforts.

By using kebab case, these examples demonstrate a clear and consistent naming convention that is both readable and suitable for various web and programming contexts.


For more information on kebab case, you can refer to this detailed [guide on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Glossary/Kebab_case) or this article on [SmartWP](https://smartwp.com/kebab-case/).

## PascalCase
PascalCase is used for naming conventions where each word starts with an uppercase letter. This style is commonly used for naming classes, methods, public properties, and interfaces in C#.

- **Purpose**: Enhances readability and provides a consistent format for naming elements that are publicly accessible or part of the overall architecture.

- **Use Cases Relevant to Our Projects**:
  - **Class Names**: All class names will use PascalCase (e.g., `UserService`, `DataProcessor`), ensuring clear identification and alignment with C# standards.
  - **Method Names**: Method names will also follow PascalCase (e.g., `FetchData`, `SaveChanges`), making them easily recognizable as functions.
  - **Interfaces**: Interfaces will be named using PascalCase and typically start with an "I" (e.g., `IConfigurationService`), distinguishing them from regular classes.
  - **Public Properties**: Public properties will use PascalCase (e.g., `UserName`, `OrderDate`), providing consistency across publicly accessible fields.

## camelCase
camelCase is used for naming conventions where the first letter is lowercase and each subsequent word starts with an uppercase letter. This style is typically used for local variables, method parameters, and private fields.

- **Purpose**: Maintains clarity and differentiation between local elements and public or architectural components, supporting a clean and organized code structure.

- **Use Cases Relevant to Our Projects**:
  - **Variables and Parameters**: Local variables and method parameters will use camelCase (e.g., `userName`, `orderDetails`), enhancing readability within methods and distinguishing them from other elements.
  - **Private Fields**: Private fields within classes often use camelCase (e.g., `configValue`, `itemCount`), keeping them distinct from public properties and adhering to internal consistency.


## GitHub Titles

To distinguish between issues and pull requests (PRs) on GitHub while following best practices, we use specific conventions for titles. This approach ensures consistency, clarity, and organization within our repositories.

- **Purpose**: These conventions are designed to enhance communication and streamline the development process, making it easier to identify and understand each item, thereby improving collaboration and efficiency.

**GitHub Issue Title:**

Format: `[Type] - [Component/Area] - [Brief Description of Problem or Need]`

Example: `Bug - User Authentication - Error When Logging In`

- **[Type]**: Indicate the type of issue, such as Bug, Feature, Story, Improvement, Task, Documentation, or Refactor.
- **[Component/Area]**: Mention the specific component, feature, or area of the project affected (e.g., User Authentication, UI, API).
- **[Brief Description of Problem or Need]**: Provide a short and clear description of the problem, need, or request.

**Pull Request (PR) Title:**

Format: `[Action] - [Component/Area] - [Brief Description of Change] (Issue ID)`

Example: `Refactor - User Authentication - Simplify Login Logic (#456)`

- **[Action]**: Specify the action being taken, such as Add, Fix, Refactor, Update, Remove, Enhance, or Document.
- **[Component/Area]**: Mention the specific component, feature, or area of the project affected (e.g., User Authentication, UI, API).
- **[Brief Description of Change]**: Provide a concise description of the change or improvement.
- **(Issue ID)**: Include the relevant issue ID in parentheses to link the PR to the corresponding issue.

**Examples:**

- **Issue Title**: `Feature - Dashboard - Add User Analytics Section`
- **PR Title**: `Add - Dashboard - User Analytics Section (#123)`

By distinguishing between the purpose of an issue (describing a problem or request) and a pull request (indicating a specific action taken to address an issue), the titles become more informative and aligned with best practices for collaborative development.

### More Examples for Issues:

1. **Bug Reports:**
   - `Bug - API - Null Pointer Exception on Empty Input`
   - `Bug - User Profile - Image Upload Fails on Large Files`
   
2. **Feature:**
   - `Feature - Dashboard - Add User Analytics Section`
   - `Feature - Notifications - Enable Push Notifications`

3. **User Stories:**
   - `Story - Shopping Cart - Save items for later in the shopping cart`
   - `Story - Notifications - Enable email alerts for important updates`


4. **Improvements:**
   - `Improvement - UI - Enhance Accessibility for Screen Readers`
   - `Improvement - Performance - Optimize Database Queries for Reports`

5. **Documentation:**
   - `Documentation - API - Add Examples for Authentication Endpoints`
   - `Documentation - Setup Guide - Update Instructions for Windows Installation`

6. **Questions:**
   - `Question - API - Clarification Needed on Rate Limiting`
   - `Question - UI - Best Practices for Custom Theming`

### More Examples for Pull Requests (PRs):

1. **Bug Fixes:**
   - `Fix - API - Handle Null Pointer Exception on Empty Input (#101)`
   - `Fix - User Profile - Correct Image Upload Logic (#202)`

2. **Feature Additions:**
   - `Add - Dashboard - User Analytics Section (#303)`
   - `Add - Notifications - Implement Push Notifications Feature (#404)`

3. **Improvements:**
   - `Enhance - UI - Improve Accessibility for Screen Readers (#505)`
   - `Optimize - Performance - Refactor Database Queries for Reports (#606)`

4. **Refactoring:**
   - `Refactor - User Authentication - Simplify Login Logic (#707)`
   - `Refactor - Codebase - Modularize CSS for Better Maintainability (#808)`

5. **Documentation Updates:**
   - `Document - API - Add Usage Examples for Authentication Endpoints (#909)`
   - `Update - Setup Guide - Revise Windows Installation Instructions (#1010)`
