# Technician & Repair Service Management System

ITS203 project — a Windows Forms desktop application for a small electronics repair shop.
Built in C# (.NET 8) with a local SQLite database.

## State of this version (Milestone 2 checkpoint)

This copy matches the Milestone 2 progress report exactly:

- Full add / edit / delete / view for Customers, Technicians, Devices and Repair Jobs
- Technician assignment and repair status workflow (Received, In Progress, Completed, Collected)
- Estimated and final cost recording, with totals on the search screen
- Input validation on all four forms (required fields, phone format, email format, no negative costs)
- Basic keyword search on the repair job list

Two items are **not yet implemented** at this checkpoint and are listed as remaining work in the report:

1. Blocking deletion of a customer or device that still has linked records
2. Search filtered by customer name, device details and status

## How to run

1. Open `TechnicianRepairSystem.sln` in Visual Studio 2022 (workload: .NET desktop development).
2. Restore NuGet packages (`Microsoft.Data.Sqlite`) — Visual Studio does this automatically on first build.
3. Press F5.

The database file `repair.db` is created automatically next to the executable on first run.

## Suggested order when testing

1. Add a customer
2. Register a device for that customer
3. Add a technician
4. Create a repair job for the device and assign the technician
5. Change the status and record the final cost
6. Open Search & Repair Summary to see totals

## Project structure

```
Models/    Person (abstract), Customer, Technician, Device (abstract) + Phone/Laptop/Tablet, RepairJob
Data/      DatabaseHelper and one repository class per entity
Utils/     Validator — shared input-validation rules
Forms/     MainForm and one management screen per entity, plus SearchForm
```
