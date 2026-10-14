# Booking System

This is a console application built with C# and .NET 10.

The application allows users to create bookings, view active bookings, search for bookings by customer name and cancel bookings. It also checks booking times, room capacity and overlapping bookings.

## Requirements

- Visual Studio 2022 or a newer version that supports .NET 10
- .NET 10 SDK
- Git

## How to run the application

1. Open Visual Studio.
2. Select **Clone a repository**.
3. Paste the repository URL:

   `https://github.com/emiliamailian/BookingSystemExam.git`

4. Click **Clone**.
5. Open `BookingSystemExam.slnx` if the solution is not already open.
6. Set `BookingSystem` as the startup project.
7. Press **Ctrl + F5** to run the application.

You can now use the menu in the console to manage bookings.

## How to run the tests

1. Open the project in Visual Studio.
2. Click **Test → Test Explorer**.
3. Click **Run All Tests**.

The project includes automated xUnit tests to check the booking functionality.

You can also run the application and tests from a terminal in the repository folder:

**Start the application:**

```bash
dotnet run --project src/BookingSystem
```

**Run the tests:**

```bash
dotnet test
```