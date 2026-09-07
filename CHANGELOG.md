# Changelog

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [2.0.0] - 2026-08-21

### Added

- Explicit property selection in datasource to optimize memory usage and improve performance
- Additional grid columns: Recipient Type Details and Hidden From Address Lists Enabled
- Finally block to ensure proper session cleanup even when errors occur
- Structured action messages for better error context
- Support for multiple delegated form categories (Exchange Administration, Exchange On-Premises)

### Changed

- Refactored datasource to use server-side filtering with Get-Recipient -Filter parameter instead of client-side Where-Object filtering for better performance
- Improved error handling with detailed error messages including line numbers and script context
- Updated session options to be more secure (SkipCACheck, SkipCNCheck, SkipRevocationCheck all set to $false)
- Optimized command imports to load only required Exchange commands (Remove-Mailcontact)
- Simplified grid columns to show more relevant information (removed FirstName, Initials, LastName, Alias fields)
- Enhanced audit logging with more detailed connection and disconnection messages
- Updated datasource and task naming convention for better clarity
- Improved variable naming consistency throughout the codebase

### Fixed

- Session cleanup now guaranteed through finally block preventing potential resource leaks
- Proper handling of empty or null error messages in error logging

## [1.0.0] - 2023-08-18

Initial release of HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Delete.

### Added

- Initial release for deleting Exchange On-Premises Mail Contacts
- Search functionality for mail contacts by name, alias, or email address
- Grid selection interface for choosing mail contacts
- Delete mail contact functionality with audit logging

### Changed

### Deprecated

### Removed

### Fixed
