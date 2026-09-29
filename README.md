# Technician & Repair Service Management System (Final Version)

ITS203 project — a Windows Forms desktop application for a small electronics repair shop.
Built in C# (.NET 8) with a local SQLite database.

## What this version contains

Everything from the Milestone 2 checkpoint, **plus the two items listed there as remaining work**:

| Proposal requirement | Status |
|---|---|
| Customer management (add / edit / search / view / delete) | Complete |
| Technician management | Complete |
| Device registration | Complete |
| Repair job creation | Complete |
| Technician assignment | Complete |
| Repair status management (Received → In Progress → Completed → Collected) | Complete |
| Repair cost management (estimated + final, with totals) | Complete |
| Search and repair summary by customer, device or status | Complete |
| Input validation | Complete |

Added in this version:

1. **Referential delete protection** — a customer with registered devices, a device with
   repair jobs, or a technician assigned to jobs cannot be deleted. The user is told exactly
   how many linked records exist and what to do first.
2. **Filtered search** — as well as the quick keyword search (which now also matches customer,
   device and technician names), the search screen offers combined filters for customer name,
   device text and status, built as a parameterised SQL query across all four tables.

## How to run

1. Open `TechnicianRepairSystem.sln` in Visual Studio 2022 (workload: .NET desktop development).
2. Restore NuGet packages (`Microsoft.Data.Sqlite`) — Visual Studio does this on first build.
3. Press F5.

`repair.db` is created automatically beside the executable on first run.

## Object-oriented design

- **Abstraction** — `Person` and `Device` are abstract base classes that cannot be instantiated directly.
- **Inheritance** — `Customer` and `Technician` inherit from `Person`; `Phone`, `Laptop`, `Tablet`
  and `OtherDevice` inherit from `Device`.
- **Polymorphism** — `GetDisplayText()` is overridden differently by `Customer` and `Technician`;
  `DeviceType` and `TypicalTurnaround` are overridden by each device subclass and used live in the
  device form.
- **Encapsulation** — fields are private and reached through properties that trim text and reject
  negative costs, so an invalid object cannot exist in memory, let alone be saved.

## Project structure

```
Models/    Person (abstract), Customer, Technician, Device (abstract) + Phone/Laptop/Tablet/Other,
           DeviceFactory, RepairJob, RepairStatus, RepairJobView
Data/      DatabaseHelper and one repository class per entity
Utils/     Validator — shared input-validation rules
Forms/     MainForm, CustomerForm, TechnicianForm, DeviceForm, RepairJobForm, SearchForm
```
