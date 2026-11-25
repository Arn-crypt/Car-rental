IF DB_ID('CarRentalDb') IS NULL CREATE DATABASE CarRentalDb;
GO
USE CarRentalDb;
GO
IF OBJECT_ID('dbo.Cars') IS NULL
CREATE TABLE dbo.Cars (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    Name NVARCHAR(100) NOT NULL,
    Type NVARCHAR(30) NOT NULL,
    DailyRate DECIMAL(10,2) NOT NULL,
    IsAvailable BIT NOT NULL DEFAULT 1
);
GO
IF OBJECT_ID('dbo.Rentals') IS NULL
CREATE TABLE dbo.Rentals (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    CarId INT NOT NULL REFERENCES dbo.Cars(Id),
    CustomerName NVARCHAR(100) NOT NULL,
    Phone NVARCHAR(30) NULL,
    PickupDate DATE NOT NULL,
    ReturnDate DATE NOT NULL,
    Total DECIMAL(10,2) NOT NULL,
    IsReturned BIT NOT NULL DEFAULT 0
);
GO
IF NOT EXISTS (SELECT 1 FROM dbo.Cars)
INSERT INTO dbo.Cars (Name, Type, DailyRate) VALUES
 ('Toyota Vios',        'Sedan',     45),
 ('Honda City',         'Sedan',     50),
 ('Toyota Fortuner',    'SUV',       95),
 ('Mitsubishi Montero', 'SUV',       90),
 ('Toyota Hiace',       'Van',       110),
 ('Nissan Urvan',       'Van',       100),
 ('Suzuki Celerio',     'Hatchback', 35),
 ('Mazda 3',            'Hatchback', 60);
GO
