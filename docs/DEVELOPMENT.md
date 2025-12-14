# Development Notes (Safe/Public)

## Local Workflow (Windows)
- MySQL runs locally through XAMPP
- phpMyAdmin is used to initialize and inspect the database
- Server configuration points to local MySQL credentials
- Lua gameplay iteration happens by editing scripts and restarting/reloading server (depending on distro support)

## Debugging Checklist
- Confirm DB connectivity (host/port/user/password/database)
- Check server logs for script load errors
- Validate schema tables exist after import
- When a feature needs engine support, implement in C++ and rebuild
